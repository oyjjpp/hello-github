## 常用Shell命令总结

### 查看包的版本

rpm -qf /usr/bin/autoconf

### 查看软件路径

whereis autoconf

### 只显示当前目录下的文件

ls -al | grep "^-"

### 查看端口使用

netstat -anl | grep "80" 