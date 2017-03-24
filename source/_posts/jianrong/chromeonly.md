---
title: 只兼容chrome浏览器的方式
date: 2016-12-13 15:02:34
categories: 兼容性
tags: [兼容性,chrome]
---

&nbsp;&nbsp;&nbsp;&nbsp;月初开始做应用工场，就是类似搜狐快站，通过在后台的拖拉点拽，diy出一个app。
&nbsp;&nbsp;&nbsp;&nbsp;考虑到拖拉点拽，最后与产品扯皮胜利，可以只兼容`chrome`，不过要屏蔽其余的浏览器。
&nbsp;&nbsp;&nbsp;&nbsp;只兼容`chrome`，连是`webkit内核`的浏览器都无需兼容，研究浏览器的`BOM`，得到如下代码：
``` javascript
if(navigator.vendor.toLowerCase().indexOf("google")<0){
	// 非chrome
}else{
	// chrome
}
```
<!--more-->
&nbsp;&nbsp;&nbsp;&nbsp;如上代码，`navigator.vendor`是获取浏览器的厂商，这个可以区分具体浏览器，试了一下，`Safari`被拦截了，OK了。
&nbsp;&nbsp;&nbsp;&nbsp;部署到服务器，QA也未测试出问题来，有天我闲来无事，找了个`windows`的360浏览器，试了一下，未被拦截，有bug！
&nbsp;&nbsp;&nbsp;&nbsp;看了一下360浏览器`navigator`，NND，与`chrome`的一毛一样。
&nbsp;&nbsp;&nbsp;&nbsp;无力感，就这样吧，反正我的网站其实没有兼容性问题……