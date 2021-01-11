# redis 常见面试题

## redis为什么那么快？

>完全基于内存的操作，可以减少读取磁盘的消耗  
>单进程的，避免了线程切换和竞态产生的消耗  
>非阻塞IO：redis采用epoll作为IO多路复用的事件模型，可以减少IO上的损耗  

## redis的数据类型有哪几种，使用了那种？是怎么使用的？

string/hash/list/set/zset

## string类型的底层数据结构是怎么样的？
