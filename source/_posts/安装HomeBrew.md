---
title: 安装HomeBrew
date: 2019-03-13 11:55:00
tags:
    - HomeBrew
---
## 简介

[HomeBrew官网](http://brew.sh/index_zh-cn.html)

HomeBrew 是 Mac OSX 上的软件包管理工具，能在Mac上便捷的安装软件和卸载软件，类似于Ubuntu的apt-get

## 安装

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

将以上命令粘贴至终端。

更新Homebrew的package数据库: brew update

搜索软件：brew search 软件名，如brew search wget

安装软件：brew install 软件名，如brew install wget

卸载软件：brew remove 软件名，如brew remove wget
