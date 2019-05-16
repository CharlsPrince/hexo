---
title: LLDB调试
date: 2019-03-13 11:51:13
tags:
    - LLDB
    - 调试
---
### po
(print object) 是LLDB中的一个命令，其主要功能是输出object-c中对象(object)的信息

### p
(print)

### expr
(expression) 能够运行时修改变量的值

### n
(next) step over

### s
(step) step into

### finish
(step) step out

### c
(continue) goto next breakpoint

### p/print/expr/expression
print as a C/C++ basic variable

### call
调用。其实上述p/po后接表达式(expression)也有调用的功能，一般只在不需要显式输出，或是无返回值时使用call，用于动态调试插入调用代码。

例如可以在viewDidLoad:里面设置断点，然后在程序中断的时候输入以下命令：
   
> call [self.view setBackgroundColor:[UIColor redColor]]

继续运行程序，view的背景颜色将变成红色！

### bt
(backtrace) 打印当前调用堆栈（crash堆栈），“bt all”可打印所有thread的堆栈（相当于command+6的Debug Session Navigation）

### image 
可用于寻址，有多个组合命令，比较实用的一种用法是寻找栈地址对应的代码（行）位置

例子:

> image lookup --address 0x000000010b9ce919

