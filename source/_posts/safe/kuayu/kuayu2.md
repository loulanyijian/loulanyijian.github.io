---
title: 跨域:（二）cookie、canvas等跨域
date: 2015-09-05 15:02:34
categories: 跨域
tags: [跨域, iframe]
---

前端跨域，除了接口的跨域之外，还有其余N多形式的跨域

### 1、iframe调用
如果iframe如果是跨域的话，就无法进行父、子界面的数据交互，无法进行dom操作、无法进行方法调用。
如果是跨域的话，子界面无法请求到父界面的location地址，但是可以改写，这个可以有效防止自己的界面被恶意网站做iframe嵌套。
iframe还有一个绝招，就是设置相应header，直接不允许跨域加载

### 2、cookie的跨域
自从localstorage出来之后，cookie很少记录缓存了，现在一般用于记录用户的登录信息，用于网站界面之间的跳转。
cookie也有域之分，也可以设置根域。
跨越接口请求，携带cookie的话，在前文中有解决方案。
利用cookie的跨域特性，一般大公司的cdn或者静态资源服务器，都会使用不同域名的服务器，免得cookie带过去，又浪费带宽，又加大了服务器解析请求头的时间。

<!-- more -->

### 3、localstorage的跨域
localstorage，是跨域，这个没法整，就做个缓存而已。

### 4、图片的跨域
这个严格说来不算是跨域，算是跨权限，很多图片供应网站，如昵图网、百度图片等，图片地址不会随意在别的网站上使用的，会出个展位图，提示无权限使用。
这个无解。

### 5、flash跨越
这个简单的很，flash有自己的安全沙箱，一般都是将crosdomain.xml，放置于.swf文件一个域下，然后就万事大吉了。

### 6、canvas跨域

canvas跨域，都是canvas图片的跨域，将界面的图片地址通过canvas进行本地输出时，会出现toDataURL访问权限问题
<img src="http://images2015.cnblogs.com/blog/393512/201611/393512-20161124155909175-37788682.png" alt="canvas图片的跨域" style="width:50%">

解决方案：
根据错误分析需要在控制头增加“Access-Control-Allow-Origin”，即允许访问源文件权限，那么我们对这个页面【注意是要输出页面的图片】这样处理：
``` javascript
var img = new Image;
img.onload = myLoader;
img.crossOrigin = 'anonymous'; //可选值：anonymous，*   
img.src = 'http://myurl.com/....';
```
或者是HTML中
``` html
<img src="" id="imgclcd" crossorigin="anonymous">
```
 核心是请求头中包含了 `Origin: "anonymous"或"*"` 字段，响应头中就会附加上 `Access-Control-Allow-Origin: *` 字段，问题解决。

### 总结：
为了安全，还是跨域的好，遇到问题，挨个解决就行。

