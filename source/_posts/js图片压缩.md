---
title: js图片压缩
date: 2019-08-21 15:14:03
tags:
    - js
    - 图片压缩
---

> 创建一个新的图片对象，在图片加载完毕后，创建一个画布，通过降低图片质量的方式重绘图片，生成新的 base64 图片

```
var img = new Image();
img.onload = function () {
  var that = this;
  // 默认按比例压缩
  var w = that.width,
    h = that.height,
    scale = w / h;
  w = that.width || w;
  h = that.height || (w / scale);
  var quality = 0.5; // 默认图片质量为0.7
  //生成canvas
  var canvas = document.createElement('canvas');
  var ctx = canvas.getContext('2d');
  // 创建属性节点
  var anw = document.createAttribute("width");
  anw.nodeValue = w;
  var anh = document.createAttribute("height");
  anh.nodeValue = h;
  canvas.setAttributeNode(anw);
  canvas.setAttributeNode(anh);
  ctx.drawImage(that, 0, 0, w, h);
  // quality值越小，所绘制出的图像越模糊
  var base64 = canvas.toDataURL('image/jpeg', quality);
  base64 = base64.replace('data:image/jpg;base64,',
    'data:image/jpeg;base64,');
  if (base64.indexOf('data:image') != 0) {
    base64 = 'data:image/jpeg;base64,' + base64
  }
}
img.src = file.content;
```
