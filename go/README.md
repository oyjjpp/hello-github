# Golang常见问题

## Golang并发机制以及它所使用的CSP并发模型

### golang中的应用

golang中channel是被单独创建并且可以在协程之间传递，两个实体同时监听一个管道，一个实体通过将消息发送到channel中，另一个实体监听到这个channel的消息则进行消费，两个实体之间是匿名，这个就实现实体中间的解耦；其中channel是同步的一个消息被发送到channel中，最终一定要被另外的实体消费掉。

Golang的CPS并发模型，是通过Goroutine和Channel来实现的  

Goroutine是Go语言中并发的执行单位，其实就是和传统概念上的“线程”类似；Channel是GO语言各个并发结构体的通信机制。

因此GPM的简要概括即为：事件循环、线程池、工作队列

## Go中对nil的Slice和空的Slice的处理是一致的吗？

nil slice和empty slice是不一致的
