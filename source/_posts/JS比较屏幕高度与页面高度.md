---
title: JS比较屏幕高度与页面高度
date: 2019-08-21 14:58:52
tags:
    - 屏幕高度
    - 页面高度
    - js
---

```
// 计算页面高度，如果页面高度不超过屏幕高度，则页面高度设置为屏幕高度
document.documentElement.style.backgroundColor = "#fff";
this.screenH = window.screen.availHeight;
this.pageH = document.documentElement.offsetHeight;
if (this.pageH < this.screenH) {
    document.documentElement.style.height = this.screenH + "px";
    document.documentElement.scrollTop = '0';
} else {
    document.documentElement.style.height = 'auto';
    document.documentElement.scrollTop = '0';
}
```

```
// 获取浏览器窗口的可视区域的宽度
function getViewPortWidth() {
      return document.documentElement.clientWidth || document.body.clientWidth;
  }
   
// 获取浏览器窗口的可视区域的高度
function getViewPortHeight() {
      return document.documentElement.clientHeight || document.body.clientHeight;
  }
  
// 获取浏览器窗口水平滚动条的位置
function getScrollLeft() {
     return document.documentElement.scrollLeft || document.body.scrollLeft;
 }
  
// 获取浏览器窗口垂直滚动条的位置
function getScrollTop() {
     return document.documentElement.scrollTop || document.body.scrollTop;
 }
```

网页可见区域宽： document.body.offsetWidth (包括边线的宽)
网页可见区域高： document.body.offsetHeight (包括边线的高)

网页正文部分上： window.screenTop
网页正文部分左： window.screenLeft


屏幕分辨率的高： window.screen.height
屏幕分辨率的宽： window.screen.width


屏幕可用工作区高度： window.screen.availHeight
屏幕可用工作区宽度： window.screen.availWidth