---
title: JS-SDK调试
date: 2017-12-15 11:19:13
tags: 
		- 微信公众号
		- JS-SDK
---

## 步骤

1、登录微信公众平台并打开在线接口调试工具和公众平台测试账号。

2、打开公众平台测试账号，里面有一栏叫JS接口安全域名的，点击修改，将里面的域名填写为你将要放置的js-sdk域名，这么说，可能有点抽象，就是说这里填写的域名其实就是你站点的域名:(==关键！！！==)

![安全域名配置](https://ws1.sinaimg.cn/large/006tNc79gy1fmh8bf2s7xj30no05n0tc.jpg)

<!-- more -->

3、打开在线调试工具，选择接口类型为基础类型，接口列表为获取`access_token接口/token`,并填入测试公众号的`appid`、`secret`,然后点击检查问题获取到`access_token`

4、获取到`access_token`后，使用postman请求以下接口

```
https://api.weixin.qq.com/cgi-bin/ticket/getticket?access_token=(填入上面获取到的access_token)&type=jsapi
```

则会得到ticket

![获取ticket](https://ws4.sinaimg.cn/large/006tNc79gy1fmh74u20x1j30mc0d0ta7.jpg)

5、拿到了ticket则可以通过[sha1加密](http://tool.oschina.net/encrypt?type=2)去获取签名了

![获取签名](https://ws4.sinaimg.cn/large/006tNc79gy1fmh7uh8mm9j30om06j0tv.jpg)

仔细看一下，你会发现jsapi_ticket中间多了个`\`，其实这个`\`是不需要的，要去掉在进行加密，明文中包含了几个参数，其中appid就不多说了，测试公众号的appid；timestamp表示生成签名的时间戳，nonceStr代表随机字符串，这两个参数在测试阶段都可以随意填写，正式环境最好还是在后台服务器中使用代码生成。

6、来到这里基本就差不多了，这时你需要一个测试的demo工程，将配置需要使用到的参数配置进去：

![配置参数](https://ws3.sinaimg.cn/large/006tNc79gy1fmh85m5c65j30fl08b3zq.jpg)

去到微信开发者工具，输入你demo的运行路径，

### 如果出现：

![签名失效](https://ws1.sinaimg.cn/large/006tNc79gy1fmh897qpvlj30gl05kgm4.jpg)

一般都是签名不正确导致的，请检查，是否那个步骤有错，实在不行，也可以重新执行2-5步骤

### 如果出现：

![不可用域名](https://ws3.sinaimg.cn/large/006tNc79gy1fmh8fxwq80j30fs05umxn.jpg)

这个情况是js接口安全域名，跟你js-sdk所在的域，不是同一个域，打开公众号测试账号看看:

![安全域名](https://ws2.sinaimg.cn/large/006tNc79gy1fmh8jmhfvaj308j04hmxe.jpg)

对比下两个域，就会发现问题。

### 如果出现:

![签名配置成功](https://ws1.sinaimg.cn/large/006tNc79gy1fmh8nw6o5mj30ew06egm6.jpg)

证明你的签名已经配置成功了，这时你再点击右上角-分享到朋友圈就会看到如下界面:

![分享朋友圈](https://ws2.sinaimg.cn/large/006tNc79gy1fmh8zu9yg9j30jn0exmyu.jpg)

你会发现显示的是微信的图标和网页的标题(有时[真机]会显示公众号的名称)，结果不是跟你的需求还不是很匹配，看一下demo里面的代码：

![分享朋友圈按钮事件](https://ws4.sinaimg.cn/large/006tNc79gy1fmh939yvabj30ig098mym.jpg)

会发现在分享api外层还包了一层点击事件，只要点击一下就会出现以下界面:

![注册点击事件](https://ws2.sinaimg.cn/large/006tNc79gy1fmh956nqg0j30fm06waaq.jpg)

发现js的接口需要被注册一下才能被调用。。。。当然，如果你不需要点击才注册，只需要将`wx.onMenuShareTimeline({ ... })`这段代码移出来，防止到`wx.ready({ ... })`中就可以了。

注册完成再点击分享到朋友圈，就会出现以下界面，这样图片、链接、标题等分享的内容就实现了自定义。

![分享朋友圈自定义内容](https://ws4.sinaimg.cn/large/006tNc79gy1fmh8yf7ufdj30kp0fhq4s.jpg)

点击发送，就可以了。

### 问题:
1、真机测试发现显示不了图片和标题，目前还不知道是什么情况，有可能是微信做了认证的限制，之前看了一篇文章，说微信6.0.2之后，必须要(被)认(打)证(劫)的公众号才能显示自定义的图片和标题---囧o(╯□╰)o囧，真坑爹=_=。

