### PHP扩展编写

### 1 为什么编写PHP扩展
使用php代码编写 请求一个数组元素的平方和
    <?php
        function array_square_sum($data){
            $sum = 0;
            foreach($data as $value){
                $sum += $value * $value;
            }
            return $sum;
        }

实际执行的时候，php zend引擎会把这段话翻译成C语言，每次都需要进行内存分配。所以性能比较差。进而，基于性能上的考虑，我们可以编写一个扩展来做这个事情。

### 2 扩展编写 
> 一个是Configulator文件，它会告诉编译器编译这个扩展至少需要哪些依赖库；第二个是实际执行的文件  
> 第二个是实际执行的文件  

#### 2.1 通过源码中的 ext_skel 可以生成扩展框架

位置：/php-src/ext/ext_skel

#### 2.2 执行扩展
    $ ./ext_skel --extname=array_square_sum
    Creating directory array_square_sum
    Creating basic files: config.m4 config.w32 .svnignore array_square_sum.c php_array_square_sum.h CREDITS EXPERIMENTAL tests/001.phpt array_square_sum.php [done].

    To use your new extension, you will have to execute the following steps:

    1.  $ cd ..
    2.  $ vi ext/array_square_sum/config.m4
    3.  $ ./buildconf
    4.  $ ./configure --[with|enable]-array_square_sum
    5.  $ make
    6.  $ ./php -f ext/array_square_sum/array_square_sum.php
    7.  $ vi ext/array_square_sum/array_square_sum.c
    8.  $ make

    Repeat steps 3-6 until you are satisfied with ext/array_square_sum/config.m4 and
    step 6 confirms that your module is compiled into PHP. Then, start writing
    code and repeat the last two steps as often as necessary.

#### 2.3 执行命令后生成的文件
执行命令之后，终端告诉我们怎么去生产新的扩展。查看一下文件内容，会发现多了几个比较重要的文件config.m4,php_array_square_sum.h，array_square_sum.c。

    [root@iZ2ze1yhgn9t43zixdpjvcZ array_square_sum]$ ll
    total 32
    -rw-r--r-- 1 root root 5582 May 11 08:26 array_square_sum.c
    -rw-r--r-- 1 root root  532 May 11 08:26 array_square_sum.php
    -rw-r--r-- 1 root root 2408 May 11 08:26 config.m4
    -rw-r--r-- 1 root root  425 May 11 08:26 config.w32
    -rw-r--r-- 1 root root   16 May 11 08:26 CREDITS
    -rw-r--r-- 1 root root    0 May 11 08:26 EXPERIMENTAL
    -rw-r--r-- 1 root root 2476 May 11 08:26 php_array_square_sum.h
    drwxr-xr-x 2 root root 4096 May 11 08:26 tests

#### 2.3 配置文件config.m4
    
    
    
### 参考
> [一步步入门编写PHP扩展][1]  
> [深入 理解PHP内核][2]  
> [与 UNIX 构建系统交互: config.m4][3]  

[1] : http://www.open-open.com/lib/view/open1392188698114.html  
[2] : http://www.php-internals.com/book/?p=index  
[3] : http://php.net/manual/zh/internals2.buildsys.configunix.php
