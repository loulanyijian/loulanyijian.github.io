---
title: chrome from memory cache 与fiddler
date: 2017-03-13 15:02:34
categories: [http]
tags: [http,chrome]
---

&nbsp;&nbsp;&nbsp;&nbsp;最近项目组阿海，满脸诧异的请教我一个奇怪的问题，情景如下：
&nbsp;&nbsp;&nbsp;&nbsp;他使用`fiddler`代理服务器上JS文件，第一次的时候，可以查看到JS请求，再刷新界面，就看不到JS请求了。
&nbsp;&nbsp;&nbsp;&nbsp;在检查确认了他fiddler代理是正确配置之后，在chrome里面实际操作一下，才想起，新版的chrome已经将http &nbsp;&nbsp;&nbsp;&nbsp;code为304的情形，都处理成了200，在network面板中查看，如下展示：
![from memory cache](https://loulanyijian.github.io/images/http1.png)
&nbsp;&nbsp;&nbsp;&nbsp;如上所示颜色比较虚的status栏，对应的size为（`from memory cache`），即从内存中的缓存获取。
&nbsp;&nbsp;&nbsp;&nbsp;之前的304状态，还是会发送http请求的，现在直接取了缓存，压根不走http请求了，抓包也看不到了。
&nbsp;&nbsp;&nbsp;&nbsp;解决办法很简单：

&nbsp;&nbsp;&nbsp;&nbsp;* 1、手动清理一下浏览器缓存
&nbsp;&nbsp;&nbsp;&nbsp;* 2、window电脑下，使用`Ctrl+F5`强刷界面

&nbsp;&nbsp;&nbsp;&nbsp;PS：在`chrome dev tools`中勾选`disable cache`，是不好使的
