---
title: npm发布组件
date: 2018-02-23 09:38:21
tags:
		- npm
		- 组件
---

## 前提条件
- 安装nodejs和npm
- 拥有一个git账号用于托管代码
- 注册一个npm账号

## 在GitHub上创建一个项目
- 新建项目，然后使用以下命令clone到本地

```
git clone https://github.com/CharlsPrince/cp-verification.git
```

<!-- more -->

## 编写组件代码
```
;
(function() {
	'use strict';

	function CPVerification() {}
	CPVerification.prototype = {
		constructor: CPVerification,
		// 校验邮箱
		isEmail: function(sEmail) {
			if (sEmail == '') { return false; }
			if (sEmail.search(/^([a-zA-Z0-9_\.\-])+@([a-zA-Z0-9_-])+((\.[a-z]{2,3}){1,2})$/) != -1) { return true; } else return false;
		},
		// 校验手机号码
		isMobile: function(sMobile) {
			return /^1[3|4|5|6|7|8|9]\d{9}$/.test(sMobile);
		},
		// 校验身份证号码 - 未严谨
		isID_Card: function(sID_Card) {
			if (sID_Card == '') { return false; }
			var RegularExp = /^[0-9]{17}[0-9A-Za-z]{1}$|^[0-9]{14}[0-9A-Za-z]{1}$/
			if (RegularExp.test(sID_Card)) { return true; } else { return false; }
		},
		// 校验必须是数字或者字母
		isNumStr: function(sNumStr) {
			var str1 = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
			var i = 0;
			for (i = 0; i < sNumStr.length; i++) {
				var onechar = sNumStr.substring(i, i + 1);
				if (!(str1.indexOf(onechar) != -1)) { return false; }
			}
			return true;
		},
		// 校验电话号码
		isTel: function(sTel) {
			var RegularExp = /^((([0-9]{4}|[0-9]{3})-)|(([0−9]4|[0−9]3)))*([0-9]{7}|[0-9]{8})$|^[0-9]{11}$/
			if (RegularExp.test(sTel)) { return true; } else { return false; }
		}
	}

	if (typeof define === 'function' && typeof define.amd === 'object' && define.amd) {

		// AMD. Register as an anonymous module.
		define(function() {
			return CPVerification;
		});
	} else if (typeof module !== 'undefined' && module.exports) {
		module.exports.CPVerification = CPVerification;
	} else {
		window.CPVerification = CPVerification;
	}
}());
```

习惯了面向对象的思维，所以在封装组件的时候可能会偏向于面向对象的写法，封装的思路有很多种，个人可以根据自己的喜好选择。

然后为了适应各种模块规范，所以在最后通过模块化导出对象:

```
if (typeof define === 'function' && typeof define.amd === 'object' && define.amd) {

		// AMD. Register as an anonymous module.
		define(function() {
			return CPVerification;
		});
	} else if (typeof module !== 'undefined' && module.exports) {
		module.exports.CPVerification = CPVerification;
	} else {
		window.CPVerification = CPVerification;
	}
```

然后终端进入组件根目录，执行`npm init`,会让你输入相应的参数，
其中version是版本信息，每次发布新版本，版本号必须大于上一次的版本号。最后输入yes就是生成一个package.json文件，这个就是组件的配置文件。

```
{
  "name": "cp-verification",
  "version": "0.0.2",
  "description": "常用的校验类代码",
  "main": "index.js",
  "directories": {
    "example": "example",
    "lib": "lib"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/CharlsPrince/cp-verification.git"
  },
  "keywords": [
    "校验",
    "cp-verification",
    "cp",
    "verification"
  ],
  "author": "CharlsPrince",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/CharlsPrince/cp-verification/issues"
  },
  "homepage": "https://github.com/CharlsPrince/cp-verification#readme"
}
```

## 组件发布
新组件发布
```
npm publish
```
更新版本发布
```
npm version 0.0.2
npm publish
```

## 发布完成
发布完成后，就可以通过npm搜索你的组件，并使用了。
```
npm search cp-verification
```
![搜索组件](https://ws3.sinaimg.cn/large/006tNc79gy1foq69vyn3gj30hw00i74c.jpg)

## 版本号规范
常规组件发布版本都是使用语义化版本，npm社区版本号规则采用的是[semver](https://semver.org/lang/zh-CN/)（语义化版本），版本格式为:主版本号.次版本号.修订号,版本号递增规则如下：

1.	主版本号：当你做了不兼容的 API 修改，
2.	次版本号：当你做了向下兼容的功能性新增，
3.	修订号：当你做了向下兼容的问题修正。

先行版本号及版本编译信息可以加到“主版本号.次版本号.修订号”的后面，作为延伸。

## 持续集成
`GitHub` 已经整合了`travis`,我们需要在项目中添加`.travis.yml`文件，在下一次`push`的之后，`travis`会定时执行`npm test`测试组件,`.travis.yml`是YAML文件，配置请看[这里](https://docs.travis-ci.com/user/languages/javascript-with-nodejs/)





