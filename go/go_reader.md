
## 环境安装
- [下载包](https://www.golangtc.com/download)

## 流行框架
- [beego](https://beego.me/)


## 常见包

### time

###  testing

 - 基础功能

    ```go
        //获取当前时间
        func getCurrentTime()  string{
        	return  time.Now().Format("2006-01-02 15:04:05")
        }
    ```

    ```go
        //获取当前时间戳
        func getCurrentTimeUnix()  int64{
            return time.Now().Unix()
        }
    ```

 - 参考
    - 1 [基准测试]（https://zhangwenbing.com/blog/golang/HyNlPG-Fq8Q）