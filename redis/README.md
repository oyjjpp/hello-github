# redis 常见问题

## redis为什么那么快？

>完全基于内存的操作，可以减少读取磁盘的消耗  
>单进程的，避免了线程切换和竞态产生的消耗  
>非阻塞IO：redis采用epoll作为IO多路复用的事件模型，可以减少IO上的损耗  

## redis的数据类型有哪几种，使用了那种？是怎么使用的？

string/hash/list/set/zset

## string类型的底层数据结构是怎么样的？

 [redis_struct](./Struct.md)

## 删除数据内存占用还是很高?

>内存分配策略局限性，一般都会分配固定的空间大小，导致实际分配的内存空间大于实际申请的，从而多出了许多不连续的空闲内存块。  
>键值对的修改、删除导致了内存的扩容或者释放，导致多余的不连续的空闲内存块。  

### 解决方案

**方案一**
重启redis（需要考虑是否进行了数据持久化）

**方案二**
要求redis>4.0  
设置自动清理  
config set activedefrag yes  

### 参考

[为什么删除数据后，Redis内存占用依然很高？](https://www.oschina.net/group/database#/detail/2371060)

## redis的分布式锁用过吗？，怎么用的？

[分布式锁](.DistributedLock.md)

## redis是怎么实现原子性的?

对于Redis而言，命令的原子性指的是：一个操作的不可以再分，操作要么执行，要么不执行。  
执行get、set以及eval等API，都是一个一个的任务，这些任务都会由Redis的线程去负责执行，任务要么执行成功，要么执行失败，这就是Redis的命令是原子性的原因。  
Redis本身提供的所有API都是原子操作，Redis中的事务其实是要保证批量操作的原子性。

## redis为什么要用单线程？

1、实现简单  
2、减少多线程上下文切换的消耗  

因为Redis是基于内存的操作，CPU不是Redis的瓶颈，Redis的瓶颈最有可能是机器内存的大小或者网络带宽；既然单线程容易实现，而且CPU不会成为瓶颈，那就顺理成章地采用单线程的方案了。

### redis 单线程的优劣势

#### 优势

1、代码清晰，处理逻辑更简单  
2、不用考虑因为多线程导致得各种锁得问题  
3、不存在多进程或者多线程导致的切换而消耗CPU

#### 劣势

无法发挥多核CPU性能，不过可以通过在单机开多个Redis实例来完善；

[Redis为什么是单线程，高并发快的3大原因详解](https://zhuanlan.zhihu.com/p/58038188)

## 最新的redis6.0用了多线程？是怎么实现的？

[Redis 6.0 新特性-多线程连环13问！](https://www.cnblogs.com/madashu/p/12832766.html)

[redis中文社区文档](http://www.redis.cn/documentation.html)
