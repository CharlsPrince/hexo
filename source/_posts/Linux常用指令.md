---
title: Linux常用指令
date: 2019-03-13 11:59:37
tags:
    - linux
---
查看端口8080的占用情况
> netstat -anp|grep 8080

查看程序占用端口情况
> netstat -anp|grep mongo
>
> netstat -anp|grep node

启动mongo数据库
> service mongod start

停止mongo数据库
> service mongod stop

允许主机上的mongodb数据被远程连接

命令行输入:

> sudo vi /etc/mongod.conf

修改文件
```
＃bind_ip = 127.0.0.1　改为bind_ip=0.0.0.0　即可通过远程连接此服务器，以前是只可以在本地连接

＃port = 27017　改为　port＝27017　即设置远程连接的端口

#auth=true 改为　auto＝true　即将权限验证连接数据库，如还需通过匿名访问或不通过权限验证访问，此处可以不改

然后重启数据库

service mongod start
```

## du 功能 - 查看磁盘空间

```
-h：以人类可读的方式显示
-a：显示目录占用的磁盘空间大小，还要显示其下目录和文件占用磁盘空间的大小
-s：显示目录占用的磁盘空间大小，不要显示其下子目录和文件占用的磁盘空间大小
-c：显示几个目录或文件占用的磁盘空间大小，还要统计它们的总和
--apparent-size：显示目录或文件自身的大小
-l ：统计硬链接占用磁盘空间的大小
-L：统计符号链接所指向的文件占用的磁盘空间大小
du -sh : 查看当前目录总共占的容量。而不单独列出各子项占用的容量 

du -lh --max-depth=1 : 查看当前目录下一级子文件和子目录占用的磁盘容量。
du -sh [目录] 查看指定子目录占用的磁盘容量
```

## 查看防火墙状态

```
service iptables status
```

## 查看缓存情况


```
free -m
```

---

## 查找文件


```
find / -name [findname]
```

## 建立软连接

```
ln -s /root/download/mongodb/bin/mongod(当前) /usr/local/bin/mongod(目标)
```

## 指定数据库日志地址

```
mongod --logpath=/data/log/mongo.log --fork
```
