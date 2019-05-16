---
title: mac命令行控制SublimeText打开文件
date: 2017-12-26 15:27:57
tags:
		- sublimeText
		- bash
---

## mac命令行控制SublimeText打开文件

### 方法一: 软链接
> sudo ln -s "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl

其中`/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl`
根据各人安装sublimeText位置不同而有所不同


### 方法二: 别名方式

打开用户配置文件，如果提示没有该文件则先执行`touch ~/.bash_profile`创建配置文件


```
vim ~/.bash_profile
```


为subl添加别名


```
alias subl='/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl'
＃也可以通过将路径添加到环境变量中实现
```

编辑完成后，`esc` + `:wq` + `enter` 退出编辑模式，然后再执行:


```
source ~/.bash_profile
```

使配置文件生效。此时在控制台上输入:

> subl -v

如果打印如下类似SublimeText版本号的文本则证明subl这个命令执行工具已经配置成功。

> Sublime Text Build 3143

也可以使用`subl -help`查看下这个工具支持什么指令。

想要在控制台控制使用SublimeText某个文件，一般是 `subl + 目的文件或文件夹路径`, 如:

>   subl ~/.bash_profile

