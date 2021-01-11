# redis底层数据结构

redis的底层数据结构包含简单的动态字符串（SDS）、链表、字典、跳跃表、压缩列表、整数集合、对象；常用的数据类型都是由一种或几种数据结构构成；命令行使用“object encoding key”可以查看key的数据结构。

## 参考

[Redis的底层数据结构](https://www.cnblogs.com/MouseDong/p/11133941.html) 
[Redis设计与实现](https://book.douban.com/subject/25900156/)
