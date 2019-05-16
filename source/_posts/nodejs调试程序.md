---
title: nodejs调试程序
date: 2019-03-13 11:43:41
tags:
---

# Chrome DevTools

```
首先在命令行输入 node --inspect ./bin/www
```

> 访问 `chrome://inspect`, 点击配置按钮，确保 Host 和 Port 对应

> 访问元信息中(http://127.0.0.1:9229/json)的 devtoolsFrontendUrl

> Chrome 打开连接 (http://127.0.0.1:9229) 然后使用 cmmand+option+i 快速打开开发者工具，点击绿色小图标