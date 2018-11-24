
## 环境安装
- [下载包](https://www.golangtc.com/download)

## 流行框架
- [beego](https://beego.me/)
- [Buffalo](https://github.com/gobuffalo/buffalo)
- [Echo](https://github.com/labstack/echo)
- [Gin](https://github.com/gin-gonic/gin)
- [Iris](https://github.com/kataras/iris)
- [Revel](https://github.com/revel/revel)
- [go实现的定时器](https://github.com/robfig/cron)

## 相关书籍

- [Go语言实战: 编写可维护Go语言代码建议](https://github.com/llitfkitfk/go-best-practice#51-%E8%80%83%E8%99%91%E6%9B%B4%E5%B0%91%E6%9B%B4%E5%A4%A7%E7%9A%84%E5%8C%85)


## 常见包

### 字符串相关

#### fmt

#### strings

#### strconv

###### 1、简介
  
strconv包实现了基本数据类型和其字符串表示的相互转换。


### bytes

###### 1、简介

bytes包实现了操作[]byte的常用函数

```go
type byte byte
8位无符号整型，是uint8的别名，二者视为同一类型。
```


###### 2、转换（大小写）
> 将 s 中的所有字符修改为大写（小写、标题）格式返回。  
func ToUpper(s []byte) []byte  
func ToLower(s []byte) []byte  
func ToTitle(s []byte) []byte  
// 使用指定的映射表将 s 中的所有字符修改为大写（小写、标题）格式返回。  
func ToUpperSpecial(_case unicode.SpecialCase, s []byte) []byte  
func ToLowerSpecial(_case unicode.SpecialCase, s []byte) []byte  
func ToTitleSpecial(_case unicode.SpecialCase, s []byte) []byte  
// 将 s 中的所有单词的首字符修改为 Title 格式返回。  
// BUG: 不能很好的处理以 Unicode 标点符号分隔的单词。  
func Title(s []byte) []byte  

    
    func bytesUpperLower()  {
    	a := []byte("I,am,is,a,gopher")
    	upper := bytes.ToUpper(a)
    
    	fmt.Printf("全部转换为大写:%q\n",upper)
    	lower := bytes.ToLower(a)
    	fmt.Printf("全部转换成小写:%q\n",lower)
    	title := bytes.ToTitle([]byte("learn go languager"))
    	fmt.Printf("全部转换成Title:%q\n",title)
    
    	fmt.Println(bytes.ToLowerSpecial(unicode.TurkishCase, []byte("dünyanın ilk borsa yapısı Aizonai kabul edilir")))
    }
    

###### 3、分割及拼接
>// Split 以 sep 为分隔符将 s 切分成多个子串，结果不包含分隔符。  
// 如果 sep 为空，则将 s 切分成 Unicode 字符列表。  
// SplitN 可以指定切分次数 n，超出 n 的部分将不进行切分。  
func Split(s, sep []byte) [][]byte  
func SplitN(s, sep []byte, n int) [][]byte  
// 功能同 Split，只不过结果包含分隔符（在各个子串尾部）。  
func SplitAfter(s, sep []byte) [][]byte  
func SplitAfterN(s, sep []byte, n int) [][]byte  
// 以连续空白为分隔符将 s 切分成多个子串，结果不包含分隔符。  
func Fields(s []byte) [][]byte  
// 以符合 f 的字符为分隔符将 s 切分成多个子串，结果不包含分隔符。  
func FieldsFunc(s []byte, f func(rune) bool) [][]byte  
// 以 sep 为连接符，将子串列表 s 连接成一个字节串。  
func Join(s [][]byte, sep []byte) []byte  
// 将子串 b 重复 count 次后返回。  
func Repeat(b []byte, count int) []byte 

    //截断
    func bytesSplit()  {
    	a := []byte("  Hello   World !  ")
    	b := []byte("I,am,is,a,gopher")
    	c := []byte("I am is a gopher")
    	d :=[][]byte{
    		a,
    		b,
    		c,
    	}
    	fmt.Printf("%q\n", bytes.Split(b, []byte{','}))
    	fmt.Printf("%q\n", bytes.SplitN(b,[]byte{','}, 3))
    
    	fmt.Printf("%q\n", bytes.SplitAfter(b, []byte{','}))
    	fmt.Printf("%q\n", bytes.SplitAfterN(b, []byte{','}, 3))
    
    	fmt.Printf("%q\n", bytes.Fields(c))
    
    	f := func(r rune) bool {
    		return bytes.ContainsRune([]byte(" o"), r)
    	}
    	fmt.Printf("%q\n", bytes.FieldsFunc(a, f))
    	//连接
    	fmt.Printf("%q\n", bytes.Join(d, []byte{'x'}))
    	//重复
    	fmt.Printf("%q\n", bytes.Repeat(a,3))
    }

######  4、清理

>// 去掉 s 两边（左边、右边）包含在 cutset 中的字符（返回 s 的切片）  
func Trim(s []byte, cutset string) []byte  
func TrimLeft(s []byte, cutset string) []byte  
func TrimRight(s []byte, cutset string) []byte  
// 去掉 s 两边（左边、右边）符合 f 要求的字符（返回 s 的切片）  
func TrimFunc(s []byte, f func(r rune) bool) []byte  
func TrimLeftFunc(s []byte, f func(r rune) bool) []byte  
func TrimRightFunc(s []byte, f func(r rune) bool) []byte  
// 去掉 s 两边的空白（unicode.IsSpace）（返回 s 的切片）  
func TrimSpace(s []byte) []byte  
// 去掉 s 的前缀 prefix（后缀 suffix）（返回 s 的切片）  
func TrimPrefix(s, prefix []byte) []byte  
func TrimSuffix(s, suffix []byte) []byte  
    
    //清理
    func bytesTrim()  {
    	bs := [][]byte{
    		[]byte("Hello World ！"),
    		[]byte("Hello 世界！"),
    		[]byte("hello golang ."),
    	}
    
    	f := func(r rune) bool{
    		return bytes.ContainsRune([]byte("!！.。"), r)
    	}
    
    	for _,b := range bs{
    		fmt.Printf("%q\n", bytes.TrimFunc(b, f))
    	}
    
    	for _, b := range bs {
    		fmt.Printf("%q\n", bytes.TrimPrefix(b, []byte("Hello")))
    	}
    
    	a := []byte(",I am a gopher,")
    	fmt.Printf("Origin:%q\n", a)
    	fmt.Printf("Trim:%q\n", bytes.Trim(a,",I"))
    	fmt.Printf("TrimRight:%q\n", bytes.TrimRight(a,","))
    	fmt.Printf("TrimLeft:%q\n", bytes.TrimLeft(a,","))
    
    	b := []byte(" I am a gopher ")
    	fmt.Printf("Origin:%q\n", b)
    	fmt.Printf("TrimSpace:%q\n", bytes.TrimSpace(b))
    }


###### 5、比较

###### 6、查询子串


### 单元测试

####  testing

###### 1、简介

测试文件包含test functions（自动化测试）, benchmark functions（基准测试）, and example functions

###### 2、自动化测试
    
    //执行所有_test.go文件
    go test
    
    //输出详细的测试信息
    go test -v
    
    //指定文件
    go test -v main.go
    
    //执行指定函数
    go test -v -test.run TestAdd
    
    //正则匹配测试函数
    go test -v -run A
    
###### 3、基准测试
	
- 执行测试命令  
    
>//执行所有测试用例
>go test -bench=.

>//仅执行基准测试用例
>//-run=none
>go test -bench=. -run=none

>//执行具体的基准测试函数(BenchmarkArray)
>go test -bench=Array -run=none

>//内容消耗情况
>//-benchmem可以提供每次操作分配内存的次数，以及每次操作分配的字节数
>go test -bench=Array -run=none -benchmem

>//正则匹配所有Plus开头的基准测试函数
>go test -bench Plus

	
 - 测试结果分析
     
>➜  test go test -v -bench=Array -run=none
>goos: linux
>goarch: amd64
>pkg: test/test
>BenchmarkArray-2 1000000  1342 ns/op
>PASS
>ok  test/test 1.368s

>//意味着循环执行了 1000000 次，每次循环花费 1342 纳秒(ns)。
    

 - 常用函数
    
>b.ResetTimer() 是重置计时器，这样可以避免for循环之前的初始化代码的干扰

###### 4、示例测试
 
	
	func ExampleHello() {
		fmt.Println("hello")
		// Output: hello
	}
	
	//不考虑输出顺序
	func ExamplePerm() {
		for _, value := range Perm(4) {
		fmt.Println(value)
		}
		// Unordered output: 4
		// 2
		// 1
		// 3
		// 0
	}

	
- 注意

**没有输出注释的示例函数被编译但不执行**。
 
###### 5、参考

 - 1 [基准测试](https://zhangwenbing.com/blog/golang/HyNlPG-Fq8Q)

### 时间

####  time

###### 1、基础功能

	（1）、获取当前时间及当前时间戳
    
    //获取当前时间
    func getCurrentTime(layout string)  string{
    	if layout == "" {
    		layout = "2006-01-02 15:04:05"
    	}
    	return  time.Now().Format(layout)
    }
    
    //result : 2018-11-14 15:00:24
        
    
    
    //获取当前时间戳
    func getCurrentTimeUnix()  int64{
    	return time.Now().Unix()
    }
    
    //result : 1542178824
    

 	（2）、将给定时间字符串转换成时间类型及时间戳
    
    //将时间字符串转换成time类型，当前时区
    func formatStringToTime(layout, value string) (time.Time, error) {
    	if layout == "" {
       		layout = "2006-01-02 15:04:05"
    	}
    	return time.ParseInLocation(layout, value, time.Now().Location())
    }
    
    //param : "", "2018-11-14 15:07:12"
    //result : 2018-11-14 15:07:12 +0800 CST
    

	（3）、将给定的时间戳转换成时间类型及时间戳    
    
    //将整型转换为time类型
    func formatIntToTime(value int64) time.Time{
    	return time.Unix(value, 0)
    }
    
    var curUnix int64= 1541997444
    curTime := formatIntToTime(curUnix)
    fmt.Printf("curUnix:%T, cutTime:%T", curUnix, curTime)
    //result : curUnix:int64, cutTime:time.Time#
    

	（4）、计算两个时间的区段
    
    //获取两个时间的时间间隔
    func getTimeSub(startTime, endTime time.Time) time.Duration{
    	return endTime.Sub(startTime)
    }
    
    //获取当前到指定时间的时间间隔
    func getTimeSince(startTime time.Time) time.Duration {
    	return time.Since(startTime)
    }
    
### 参考
- 1 [Golang包](https://www.cnblogs.com/golove/tag/Golang%E5%8C%85/)

