### 错误与异常

    <?php
    $num = 0;
    try {
    	echo 1/$num;
    } catch (Exception $e){
    	echo $e->getMessage();
    }


#### 问题
什么是错误？什么是异常？  
try catch 能捕获的是什么？  

#### 错误级别

    1     E_ERROR           致命的运行错误。错误无法恢复，暂停执行脚本。  
    2     E_WARNING         运行时警告(非致命性错误)。非致命的运行错误，脚本执行不会停止。  
    4     E_PARSE           编译时解析错误。解析错误只由分析器产生。  
    8     E_NOTICE          运行时提醒(这些经常是你代码中的bug引起的，也可能是有意的行为造成的。)  
    16    E_CORE_ERROR PHP  启动时初始化过程中的致命错误。  
    32    E_CORE_WARNING    PHP启动时初始化过程中的警告(非致命性错)。  
    64    E_COMPILE_ERROR   编译时致命性错。这就像由Zend脚本引擎生成了一个E_ERROR。  
    128   E_COMPILE_WARNING 编译时警告(非致性错)。这就像由Zend脚本引擎生成了E_WARNING警告。  
    256   E_USER_ERROR      自定义错误消息。像用PHP函数trigger_error（程序员设置E_ERROR）  
    512   E_USER_WARNING    自定义警告消息。像用PHP函数trigger_error（程序员设的E_WARNING警告）   
    1024  E_USER_NOTICE     自定义的提醒消息。像由使用PHP函数trigger_error（程序员E_NOTICE集）  
    2048  E_STRICT          编码标准化警告。允许PHP建议修改代码以确保最佳的互操作性向前兼容性。   
    4096  E_RECOVERABLE_ERROR   开捕致命错误。像E_ERROR，但可以通过用户定义的处理捕获（又见set_error_handler（））  
    8191  E_ALL             所有的错误和警告(不包括 E_STRICT) (E_STRICT will be part of E_ALL as of PHP 6.0)  
    16384 E_USER_DEPRECATED   
    30719 E_ALL  

    E_All： 十进制为30719，换成二进制为 111011111111111  
    E_NOTICE：十进制为8，换成二进制为 1000  
    ~E_NOTICE：对E_NOTICE进行取反操作, 变成0111  
    E_ALL & ~E_NOTICE:：E_ALL和 ~E_NOTICE进行与操作，变成111011111110111，化成十进制就是30711  

#### 错误处理函数及设置

###### 1、error_reporting()
用于运行时设置PHP的报错级别或者返回当前级别  
function error_reporting ($level = null) {}  

    error_reporting(E_ERROR|E_PARSE|E_COMPILE_ERROR|E_CORE_ERROR|E_USER_ERROR);  
    error_reporting(E_ALL & ~E_NOTICE);  
    $errLevel = error_reporting();

###### 2、display_errors设置
错误回显，一般常用语开发模式，但是很多应用在正式环境中也忘记了关闭此选项。错误回显可以暴露出非常多的敏感信息，为攻击者下一步攻击提供便利。推荐关闭此选项。 一旦某个产品投入使用，那么第一件事就是应该将display_errors选项关闭，以免因为这些错误所透露的路径、数据库连接、数据表等信息而遭到黑客攻击。  
On表示开启状态下，若出现错误，则报错，出现错误提示。 Off 表示关闭状态下，若出现错误，则提示：服务器错误。但是不会出现错误提示

    ini_set('display_errors', 'on');  
    ini_set('display_errors', 'off');

###### 3、log_errors设置
生产环境下开启log_errors，把错误信息记录在日志里;可以关闭错误回显。

    # vim /etc/php.ini
    display_errors = Off
    log_errors = On
    error_log = /var/log/php-error.log


###### 4、set_error_handler()
设置运行期间自定义错误处理函数  
mixed set_error_handler ( callable $error_handler [, int $error_types = E_ALL | E_STRICT ] )

*使用*
>//直接传函数名 NonClassFunction  
set_error_handler('function_name');  
//传class_name && function_name  
set_error_handler(array('class_name', 'function_name'));

*注意*
>使用该函数后就不能使用error_reporting()设置错误level  
如果函数返回 FALSE，标准错误处理处理程序将会继续调用  

###### 5、set_exception_handler()
设置运行期间自定义异常处理函数，用于捕获没有被try/catch捕获的异常  
set_exception_handler ( callable $exception_handler )  

###### trigger_error()
产生一个用户级别的error/warning/notice信息  
trigger_error ( string $error_msg [, int $error_type = E_USER_NOTICE ] )

*使用*
>trigger_error("Cannot divide by zero", E_USER_ERROR);

#### 异常与错误



#### Throwable、Exception、Error的关系

#### PHP如何捕获异常

>try{}catch(){}  
异常捕获步骤  
1、被匹配的try catch 结构捕获  
2、调用异常处理函数  set_exception_handler().  register_shutdown_function  set_error_handler  
3、被报告为一个致命错误(Fatal Error)  

#### 注意

抛出的异常必须为Exception类或者Exception的子类  
错误不能被try catch捕获

#### 参考  

 - [再谈PHP错误与异常处理](https://www.cnblogs.com/zyf-zhaoyafei/p/6928149.html#excetion3)
 - [HP 的异常处理、错误处理](https://blog.csdn.net/aerchi/article/details/37757751)
 - [PHP错误处理函数set_error_handler()的用法](https://www.cnblogs.com/52php/p/5659961.html)
