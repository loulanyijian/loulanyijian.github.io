---
title: https改造:（二）实际动手
date: 2017-04-09 15:02:34
categories: http
tags: [https]
---

动手！
### 关于JS与css
如果在一个HTTPS页面里动态的引入HTTP资源，比如引入一个js文件，会被直接block掉的。
css的话，也是会在控制台报错，直接加载不了。
这个由于我们使用了乐视的CDN，上传JS的时候，可以直接同步http与https，

### 关于图片
https页面中可引用http的图片，虽然不会报红错，但是会有黄色的提醒。
最好的方法是使用https的资源。也是使用乐视CDN的双协议方法。

### 关于接口

<!-- more -->

如果在https的页面中使用http的ajax调用。会提示跨域的报错，很明显有违ip地址、端口、协议的跨域限制。
jsonp也解决不了跨域，因为jsonp的原理是加载JS，JS也不能跨协议加载
所以，直接一步到位，后台服务接口，也改成https的

### a标签
这个还是好用的，即使是https的页面也可以跳转到http的链接。

### 页面引用
既然我们的静态文件支持了http和https两种协议。但是静态文件并不知道页面是什么协议。我们应该怎么适应呢？引用资源的url中我们应该使用相对协议，比如

`src=//a.com/static/a.js`

### 其余跨域问题
跨域很明白了，不是一个协议的，就算是跨域，so，`http://www.a.com`，与h`ttps://www.a.com`，完全跨域，包括`cookie`、`localstorage`什么的，全部不能共享。

### 后台返回的绝对地址
如果后台返回、前端渲染地址，需要通过正则处理掉，如
`(“http://abc.com/index.html”).replace(/http:/g, "")`


参考链接:
[前端静态文件如何应对HTTPS的到来](http://www.cnblogs.com/webARM/p/5728695.html)