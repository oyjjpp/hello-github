# 数据同步

redis的高可用，一个是使用AOF或RDB保证数据减少丢失，另一个是是通过增加副本减少服务的中断

## 主从库读写分离

保证所有数据实例的一致性，只有主库可以进行写入，主从库都可以进行读操作。
![image](./image/master_slave_read_write.jpg)

## 主从同步流程

第一阶段，是主从库间建立连接、协商同步的过程，主要是为全量复制做准备。  
第二阶段，主库将所有数据同步给从库,从库收到数据后，在本地完成数据加载,这个过程依赖于内存快照生成的RDB文件。  
第三阶段，主库会把第二阶段执行过程中新收到的写命令，再发送给从库。具体的操作是，当主库完成 RDB 文件发送后，就会把此时 replication buffer 中的修改操作发给从库，从库再重新执行这些操作。这样一来，主从库就实现同步了。

![image](./image/master-slave.jpg)

## 主从同步的模式

### 全量复制  

全量复制虽然耗时，但是对于从库来说，如果是第一次同步，全量复制是无法避免的，所以，我给你一个小建议：一个 Redis 实例的数据库不要太大，一个实例大小在几 GB 级别比较合适，这样可以减少 RDB 文件生成、传输和重新加载的开销。另外，为了避免多个从库同时和主库进行全量复制，给主库过大的同步压力，我们也可以采用“主 - 从 - 从”这一级联模式，来缓解主库的压力。

基于长连接的命令传播：  
长连接复制是主从库正常运行后的常规同步阶段。在这个阶段中，主从库之间通过命令传播实现同步。

增量复制：
主从库之间通过命令传播实现同步这期间如果遇到了网络断连，增量复制就派上用场了。我特别建议你留意一下 repl_backlog_size 这个配置参数。如果它配置得过小，在增量复制阶段，可能会导致从库的复制进度赶不上主库，进而导致从库重新进行全量复制。所以，通过调大这个参数，可以减少从库在网络断连时全量复制的风险。

## 哨兵机制：主库挂了，如何不间断服务？

主库真的挂了吗？该选择哪个从库作为主库？怎么把新主库的相关信息通知给从库和客户端呢？

### 哨兵机制的基本流程

哨兵其实就是一个运行在特殊模式下的 Redis 进程，主从库实例运行的同时，它也在运行。哨兵主要负责的就是三个任务：监控、选主（选择主库）和通知。

## 什么主从库间的复制不使用 AOF？

1、RDB文件时二进制，无论是把RDB存入磁盘，还是通过网络传输，IO效率都会比AOF高  
2、从库恢复时RDB比AOF快  