# Golang常见问题

## Golang中出了加Mutex锁之外还有哪些方式安全读写共享变量

1、atomic包提供了原子性内存原语  
2、可以使用channel在go协程中安全读写共享变量  

## 无缓冲chan的发送和接收是否同步

```golang
ch := make(chan int) // 无缓冲的channel由于没有缓冲发送和接收需要同步
ch := make(chan int, 2) // 有缓冲channel不要求发送和操作同步
```

channel无缓冲时：发送阻塞直到数据被接收，接收阻塞直到读到数据  
channel有缓冲时：当缓冲满时发送阻塞，当缓冲空时接收阻塞  

## Golang并发机制以及它所使用的CSP并发模型

### CSP

通信顺序过程（CSP）是一种描述并发系统中交互模式的正式语言，它是并发数据理论家族中的一个成员，被称为过程算法，是基于消息的通道传递理论。

不同传统的多线程共享内存来通信，CPS讲究的是“以通信的方式来共享内存”；用于描述多个独立的并发实体通过共享的通讯管道（channel）进行通信的并发模型，CSP中channel是第一类对象，它不关注发送消息的实体，而关注与发送消息时使用的channel。

### golang中的应用

golang中channel是被单独创建并且可以在协程之间传递，两个实体同时监听一个管道，一个实体通过将消息发送到channel中，另一个实体监听到这个channel的消息则进行消费，两个实体之间是匿名，这个就实现实体中间的解耦；其中channel是同步的一个消息被发送到channel中，最终是一定要被另外的实体消费掉。

## Goroutine

Goroutine是golang实际并发执行的实体，底层是使用协程（coroutine）实现并发，coroutine是一种运行在用户态的用户线程；
它具有如下特点：  
>1、使用用户空间，可以避免了内核态和用户态的切换的成本  
>2、可以由语言和框架层进行调度  
>3、占用更小的栈空间，允许创建大量的实体  

### golang中goroutine的特性

Golang内部有三个对象：  
P对象（processor）代表上下文或者可以认为是CPU  
M对象（workthread）代表工作线程  
G对象（goroutine）

正常情况下一个cpu对象开启一个工作线程对象，线程去检查并执行goroutine对象；碰到goroutine对象阻塞的时候，会开启一个新的工作线程，充分利用cpu资源，所以有时候线程对象会比处理器对象多很多