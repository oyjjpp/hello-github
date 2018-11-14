
## 环境安装
- [下载包](https://www.golangtc.com/download)

## 流行框架
- [beego](https://beego.me/)
- [go实现的定时器](https://github.com/robfig/cron)

## 常见包

###  testing

  - 简介

    测试文件包含test functions（自动化测试）, benchmark functions（基准测试）, and example functions

  - 自动化测试

  - 基准测试

    - 1 执行测试命令
      ```go
            //执行所有测试用例
            go test -bench=.

            //仅执行基准测试用例
            go test -bench=. -run=none

            //执行具体的基准测试函数(BenchmarkArray)
            go test -bench=Array -run=none
      ````

    - 2 测试结果分析

        ```go
            ➜  test go test -v -bench=Array -run=none
            goos: linux
            goarch: amd64
            pkg: test/test
            BenchmarkArray-2         1000000              1342 ns/op
            PASS
            ok      test/test     1.368s

            //意味着循环执行了 1000000 次，每次循环花费 1342 纳秒(ns)。
        ```

  - 示例测试

  - 参考
    - 1 [基准测试](https://zhangwenbing.com/blog/golang/HyNlPG-Fq8Q)

###  time

 - 基础功能

    - 1 获取当前时间及当前时间戳
    ```go
        //获取当前时间
        func getCurrentTime(layout string)  string{
            if layout == "" {
                layout = "2006-01-02 15:04:05"
            }
            return  time.Now().Format(layout)
         }

         //result : 2018-11-14 15:00:24
    ```

    ```go
        //获取当前时间戳
        func getCurrentTimeUnix()  int64{
            return time.Now().Unix()
        }

        //result : 1542178824
    ```

    - 2 将给定时间字符串转换成时间类型及时间戳
    ```go
        //将时间字符串转换成time类型，当前时区
        func formatStringToTime(layout, value string) (time.Time, error) {
            if layout == "" {
                   layout = "2006-01-02 15:04:05"
            }
            return time.ParseInLocation(layout, value, time.Now().Location())
        }

        //param : "", "2018-11-14 15:07:12"
        //result : 2018-11-14 15:07:12 +0800 CST
    ```

    - 3 将给定的时间戳转换成时间类型及时间戳
    ```go
        //将整型转换为time类型
        func formatIntToTime(value int64) time.Time{
            return time.Unix(value, 0)
        }

        var curUnix int64= 1541997444
        curTime := formatIntToTime(curUnix)
        fmt.Printf("curUnix:%T, cutTime:%T", curUnix, curTime)
        //result : curUnix:int64, cutTime:time.Time#
    ```

    - 4 计算两个时间的区段
    ```go
        //获取两个时间的时间间隔
        func getTimeSub(startTime, endTime time.Time) time.Duration{
            return endTime.Sub(startTime)
        }

        //获取当前到指定时间的时间间隔
        func getTimeSince(startTime time.Time) time.Duration {
            return time.Since(startTime)
        }
    ```


