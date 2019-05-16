---
title: Cordova概要
date: 2017-06-23 20:30:50
tags:
		- 混合开发
		- Cordova
---

## 安装Cordova CLI
1. 下载和安装Node.js。安装完成后你可以在命令行中使用node 和 npm 。
2. (可选)下载和安装git client, 如果你没有。安装成功后，你可以在命令行中使用git。 这个命令行使用下载git仓库中的资源。
3. 安装cordova 模块使用Nodejs的npm工具。cordova模块会被npm工具自动下载。

<!-- more -->

- 在OS X和Linux上:
```
$ sudo npm install -g cordova
```
在OS X和Linux上, npm命令加上前缀sudo因为cordova可能需要安装在其他的受限制目录比如 /usr/local/share。如果你使用可选工具nvm/nave或者具有安装目录的写权限，那么你可以省略sudo前缀。这里有更多提示 可用在使用 npm 没有 sudo前缀时，如果你想那么做。

- 在Windows上:
```
C:\>npm install -g cordova
```
`-g` 标志是告诉 `npm` 我们全局安装 `cordova`。否则我们将会安装在当前工作目录的 `node_modules` 子目录。

安装完成后，你应该能够在命令行中运行`cordova`命令，在没有任何参数的时候会打印一些帮助信息。

## 创建App
cd 到你想要保存的项目路径，使用一下命令创建cordova项目:
```
$ cordova create hello com.example.hello HelloWorld
```

## 添加平台
- cd 到项目根目录

```
$ cd hello
```
- 给你的App添加目标平台。我们将会添加'ios'和'android'平台，并确保他们保存在了config.xml中:

```
$ cordova platform add ios --save
$ cordova platform add android --save
```
- 检查你当前平台设置状况:

```
$ cordova platform ls
```

## 构建App

默认情况下, cordova create生产基于web应用程序的骨架，项目开始页面位于www/index.html 文件。任何初始化任务应该在www/js/index.js文件中的deviceready事件的事件处理函数中。

运行下面命令为所有添加的平台构建:


```
$ cordova build 
```

你可以在每次构建中选择限制平台范围 - 这个例子中是'ios':


```
$ cordova build ios
```

## 启动服务

```
$ cordova serve ios
```


## 模拟器运行

```
$ cordova emulate ios
## 指定模拟器版本 ##
$ cordova emulate ios --target iPhone-6s
$ cordova emulate ios --target iPhone-6s-Plus
```


## 真机调试
先装ios-deploy:
```
npm install -g ios-deploy
```
再配置好证书之类的，然后运行：
```
cordova run ios --device
```

## 插件

### 插件常用命令:

#### 查看所有已经安装的插件

```
cordova plugin ls
```

#### 安装插件(如)

```
cordova plugin add cordova-plugin-camera
```

#### 删除插件

```
cordova plugin rm cordova-plugin-camera
```

#### 更新插件

```
cordova plugin update
```

### 常用插件
#### 1，Console（调试控制台）

让程序可以在控制台中打印输出日志。

```
cordova plugin add cordova-plugin-console
```

#### 2，Connection（网络连接）

用来判断网络连接类型（2G、3G、4G、Wifi、无连接等）


```
cordova plugin add cordova-plugin-network-information
```


#### 3，Device（设备）

获取一些设备信息。


```
cordova plugin add cordova-plugin-device
```


#### 4，Hardware

Nofifications（硬件消息提醒）
让设备蜂鸣或振动。


```
cordova plugin add cordova-plugin-vibration
```


#### 5，Visual Notification（可视化消息提醒）

不同于js的alert()、confirm()和prompt()方法是同步的。Cordova的alert()、confirm()和prompt()方法是异步的，并且对显示内容有更大的控制权限。


```
cordova plugin add cordova-plugin-dialogs
```


#### 6，Battery（电池）

可以获取电池状态信息。


```
cordova plugin add cordova-plugin-battery-status
```


#### 7，Accelerometer(加速计)

让应用在三维空间(使用笛卡尔三维坐标系统)中决定设备方向。

```
cordova plugin add cordova-plugin-device-motion
```


#### 8，Compass(指南针)

可以让开发者读取移动设备的朝向。


```
cordova plugin add cordova-plugin-device-orientation
```


#### 9，Geolocation(地理定位)

让应用判断设备的物理位置。


```
cordova plugin add cordova-plugin-geolocation
```


#### 10，Camera(相机)

用相机获取图像。


```
cordova plugin add cordova-plugin-camera
```


#### 11，Media Capture （媒体捕获）

与Camera API相比，不仅能获取图像，还可以录视频或者录音。


```
cordova plugin add cordova-plugin-media-capture
```


#### 12，Globalization(全球化)

允许应用查询操作系统的当前设置，判断用户使用的语言。


```
cordova plugin add cordova-plugin-globalization
```


#### 13，Contacts（联系人）

读取联系人列表并在应用中使用联系人数据，或使用应用数据向联系人列表中写新的联系人。


```
cordova plugin add cordova-plugin-contacts
```


#### 14，Media（播放/记录媒体文件）

让应用能记录或播放媒体文件。用它可以在手机后台播放音频文件或玩桌面视频游戏。


```
cordova plugin add cordova-plugin-media
```


#### 15，InAppBrowser（内置浏览器）

允许在在单独的窗口中加载网页。例如要向应用用户展示其他网页。当然可以很容易地在应用中加载网页内容并管理，但有时候需要不同的用户体验，InAppBrowser加载网页内容，应用用户可以更方便的直接返回到主应用。


```
cordova plugin add cordova-plugin-inappbrowser
```


#### 16，Splashscreen（闪屏）

用来在Cordova应用启动时显示自定义的闪屏。


```
cordova plugin add cordova-plugin-splashscreen
```


#### 17，exitApp（退出应用）

让 Android 或者 Windows Phone 8 上的APP关闭退出（iOS系统不支持）。


```
cordova plugin add cordova-plugin-exitapp
```


#### 18，barcodeScanner（条形码/二维码扫描）

不仅可以通过摄像头识别二维码/条形码，还能生成二维码。


```
cordova plugin add cordova-plugin-barcodescanner
```


#### 19，file（文件访问操作类）

提供对设备上的文件进行读取和写入的功能支持。


```
cordova plugin add cordova-plugin-file
```


#### 20，fileTransfer（文件传输）

实现文件上传、下载及共享等功能。


```
cordova plugin add cordova-plugin-file-transfer
```

