---
title: Mac node.js环境的安装与测试
date: 2017-12-16 18:08:11
tags:
		- node.js
---

## 1、mac node.js环境的配置
第一步：打开终端，输入以下命令安装Homebrew
~~~
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
~~~
Homebrew官网 http://brew.sh/index_zh-cn.html
![Homebrew 安装成功.png](http://upload-images.jianshu.io/upload_images/2925367-8c429114bbd9931c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!-- more -->

第二步：安装node,在终端输入以下命令
~~~
brew install node
~~~

![安装 node.png](http://upload-images.jianshu.io/upload_images/2925367-ea7f099b5323db3d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

第三步：查看node安装是否成功

![查看node版本.png](http://upload-images.jianshu.io/upload_images/2925367-63b6ad3abdedf946.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2、新建测试程序
第一步：新建一个文件test.js
~~~
var http = require('http');

var data = {key : 'value', hello: 'world'};

var srv = http.createServer(function (req, res) {
	res.writeHead(200, {'Content-Type': 'application/json'});
	res.end(JSON.stringify(data));
});

srv.listen(8080, function() {
	console.log('listening on localhost:8080');
});
~~~

第二步：用终端找到其所在的文件目录运行
~~~
 node Desktop/test.js listen on localhost:8080
~~~

第三步：通过浏览器进行访问，返回json格式的数据

![浏览器访问.png](http://upload-images.jianshu.io/upload_images/2925367-fcf6e2be43ae0e51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

第四步：前端就可以通过这个接口进行数据解析了。

非常感谢：[李玉刚博客(mac 上node.js环境的安装与测试)](http://blog.csdn.net/baihuaxiu123/article/details/51868142)

