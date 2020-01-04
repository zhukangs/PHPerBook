# 问题与简答

## Linux篇

### Linux 目录结构

```
/
├── bin #存放二进制可执行文件，常用命令一般都在这里
├── boot #存放用于系统引导时使用的各种文件
├── dev #用于存放设备文件
├── etc #存放系统管理和配置文件
├── home #存放所有用户文件的根目录
├── lib #存放着和系统运行相关的库文件
├── media #linux 系统会自动识别一些设备，当识别后，linux 会把识别的设备挂载到这个目录下
├── mnt #用户临时挂载其他的文件系统
├── opt #额外安装的可选应用程序包所放置的位置
├── proc #虚拟文件系统目录，是系统内存的映射。可直接访问这个目录来获取系统信息
├── root #超级用户的主目录
├── run #是一个临时文件系统，存储系统启动以来的信息
├── sbin #存放二进制可执行文件，只有 root 才能访问
├── srv #该目录存放一些服务启动之后需要提取的数据
├── sys #存放内核相关文件
├── tmp #用于存放各种临时文件，是公用的临时文件存储点
├── usr #用于存放系统应用程序
└── var #用于存放运行时需要改变数据的文件，比如服务的日志文件
```

### Linux基础

查看系统信息、内存信息、磁盘信息、负载信息、路由信息、端口信息、进程、登录用户、关机、重启、系统时间、用户管理、文件权限、压缩解压

### 命令与文件查找

- which 寻找可执行文件

```shell
[root@localhost ~]# which php
/usr/bin/php
```

- whereis-特定目录寻找

```shell
whereis php
php: /usr/bin/php /usr/lib64/php /etc/php.d /etc/php.ini /usr/include/php /usr/share/php /usr/share/man/man1/php.1.gz
```

- find-直接搜索硬盘

```shell
[root@localhost ~]# find / -name php-fpm
/run/php-fpm
/etc/sysconfig/php-fpm
/etc/logrotate.d/php-fpm
/var/log/php-fpm
/usr/sbin/php-fpm
```

### 简述Linux下安装PHP的过程 

```shell
安装软件之前先安装编译工具gcc、gcc-c++
拷贝源码包，解包解压缩
Cd /lamp/php进入php目录
./configure –prefix=/usr/local/php –with-config-file-path=/usr/local/php/etc指定安装目录和配置文件目录
Make 编译
Make install安装
```

### 简述Linux下安装Mysql的过程

```shell
Groupadd mysql 添加一个用户组mysql
Useradd -g mysql mysql 添加一个mysql用户指定分组为mysql
Cd /lamp/mysql 进入mysql目录
./configure –prefix=/usr/local/mysql/ –with-extra-charsets=all
Make
Make all
```

### 简述Linux下安装apache的过程

```shell
Cd /lamp/httpd 进去apache软件目录
./configure –prefix=/usr/local/apache2/ –sysconfdir=/etc/httpd/ –with-included-apr
Make
Make all
```

### 推荐阅读资料

- [Linux学习归纳](https://www.zam9.com/blog/Linux01)

