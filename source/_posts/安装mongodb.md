---
title: 安装mongodb
date: 2019-03-13 11:47:02
tags:
    - mongodb
---

## 安装MongoDB

## Mac环境

### 1、下载安装

### 2、HomeBrew方式安装

官方文档参考: [install-mongodb-on-os-x](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

在命令行输入并执行以下:

```
$ brew install mongodb
```

启动mongodb:

```
mongod —config /usr/local/etc/mongod.conf
```

## Linux环境


```
设置源
[root@vm11 ~]# cd /etc/yum.repos.d/
[root@vm11 yum.repos.d]# vi mongodb-org-3.6.repo
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc

执行安装
[root@vm11 yum.repos.d]# sudo yum install -y mongodb-org

启动数据库
[root@vm11 yum.repos.d]# service mongod start
Redirecting to /bin/systemctl start mongod.service

[root@iZwz9btqnhlgt7dsj8hhhhZ nodejs]# nohup mongod &
[1] 26658
[root@iZwz9btqnhlgt7dsj8hhhhZ nodejs]# nohup: ignoring input and appending output to `nohup.out'

关闭数据库
[root@iZwz9btqnhlgt7dsj8hhhhZ nodejs]# nohup mongod --shutdown &
[1] 26636
[root@iZwz9btqnhlgt7dsj8hhhhZ nodejs]# nohup: ignoring input and appending output to `nohup.out'

查看状态
[root@vm11 yum.repos.d]# ps aux | grep mongod
mongod    1267  0.4  7.8 1010008 80184 ?       Sl   11:47   0:36 /usr/bin/mongo  -f /etc/mongod.conf
```
