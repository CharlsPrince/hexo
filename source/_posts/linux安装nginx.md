---
title: linux安装nginx
date: 2019-03-13 11:49:26
tags:
    - linux
    - nginx
---
## linux安装nginx

依次执行:

```
yum install gcc-c++
yum install -y openssl openssl-devel
yum install -y pcre pcre-devel
yum install -y zlib zlib-devel
yum -y install nginx
sudo nginx
```


如果出现:
![image](https://ws2.sinaimg.cn/large/006tNc79gy1fow6a128s5j30kg0233z3.jpg)

则 去到 /etc/nginx/conf.d 目录下，将下图框内容注释即可:
![image](https://ws3.sinaimg.cn/large/006tNc79gy1fow6byv1mej30c3065t9a.jpg)
