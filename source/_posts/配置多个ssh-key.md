---
title: 配置多个ssh key
date: 2019-05-15 19:53:04
tags:
    - ssh key
---

# SSH
## 简介
SSH 是 Secure Shell 的缩写，有 IETF 的网络小组所制定，是一种网络协议，用于计算机之间的加密登录，利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题，之所以保证安全，是因为它采用了公钥加密的方式。
## 过程
（1）远程主机收到用户的登录请求，将自己的公钥发给用户。
（2）用户使用这个公钥，将登录密码加密后发送回来。
（3）远程主机用自己的私钥，解密登录密码，如果密码正确就同意用户登录。

<!-- more -->

# 适用场景
## 同时拥有 gitlab 和 github 的账号，且注册账号的邮箱不同，而适用 ssh 生成 key ,默认会在用户的根目录下的`.ssh`文件夹下生成 id_rsa 和 id_rsa.pub 文件，但是想换一个账号 clone 代码又提示没有权限
```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

# 步骤
## 生成并添加第一个 ssh key
前往 `~/.ssh` 路径下，如果里面有文件则全部清除，然后输入以下命令，生成对应的私钥和公钥
```
$ ssh-keygen -t rsa -C "email@yourcompany.com"
```
然后需要你为其取个名字 `Enter file in which to save the key (/Users/charls/.ssh/id_rsa)` 这个随便写就行了，默认不填写的话生成的文件就是以 `id_rsa` 开头，生成了以后，将`.pub`文件的内容复制到github(gitlab)上

## 生成并添加第二个 ssh key
步骤跟第一个步骤一样，但有点需要注意的是要保证两个`key`的名称不能一样。

## 修改配置文件
因为前面已经删除了`~/.ssh`路径下的所有文件，所以应该这个路径下的文件都是新的
- 在 `~/.ssh`目录下新建一个 config 文件(无后缀)

```
$ touch config
```

- 添加内容

```
#github配置
Host github.com
    HostName ssh.github.com
    Port 443
    IdentityFile ~/.ssh/id_rsa_961629701
    User git
#gitlab的配置
Host 112.94.224.231
    HostName 112.94.224.231
    IdentityFile ~/.ssh/id_rsa_gitlab
#gitlab的配置
Host 192.168.10.85
    HostName 192.168.10.85
    IdentityFile ~/.ssh/id_rsa_gitlab
```

- ssh连接测试

```
ssh -T git@github.com
控制台会打印:
Hi CharlsPrince! You've successfully authenticated, but GitHub does not provide shell access.

ssh -T git@112.94.224.231
控制台会打印:
Welcome to GitLab, 黄佑成!

ssh -T git@192.168.10.85
控制台会打印:
Welcome to GitLab, 黄佑成!
```

# 目录结构
![目录结构](https://ws4.sinaimg.cn/large/006tNc79gy1g329zv9f1pj317o0nsdng.jpg)