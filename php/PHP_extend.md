### PHP扩展编写

#### 编写扩展

##### 需要两个文件  
> 一个是Configulator文件，它会告诉编译器编译这个扩展至少需要哪些依赖库；第二个是实际执行的文件
> 第二个是实际执行的文件  

##### 通过源码中的 ext_skel 可以生成扩展框架

位置：/php-src/ext/ext_skel

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


#### 参考
> [一步步入门编写PHP扩展][1]
> [深入 理解PHP内核][2]

[1] : http://www.open-open.com/lib/view/open1392188698114.html
[2] : http://www.php-internals.com/book/?p=index  
