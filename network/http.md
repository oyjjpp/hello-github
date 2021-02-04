# HTTP

## HTTP定义

超文本传输

![image](./image/http-history.webp)

### http1.0与http1.1的区别

1、缓存处理：http1.0增加了更多类型缓存策略  
2、数据传输优化：http1.1支持断点续传，范围请求  
3、错误状态：http1.1增加了等多响应状态  
4、长连接：HTTP1.1支持长连接（PersistentConnection）和请求的流水线（Pipelining）处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在HTTP1.1中默认开启Connection： keep-alive，一定程度上弥补了HTTP1.0每次请求都要创建连接的缺点。

## HTTPS

## 参考

[HTTP1.0、HTTP1.1和HTTP2.0的区别](https://www.jianshu.com/p/be29d679cbff)  
