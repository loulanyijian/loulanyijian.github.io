---
title: 由乐视CDN看前端性能优化
date: 2016-01-04 15:02:34
categories: 性能优化
tags: [性能,CDN]
---

最近，我们的系统告别了自己搭建静态服务器的时代，开始对接乐视网的CDN，以做更好的静态加速。
乐视网CDN的特点：
* 1、强缓存时间1年整，`Cache-Control:max-age=31536000`
* 2、每次上线，地址不一样，格式为`http://js.letvcdn.com/lc02_lecloud/201511/25/09/39/xx.min.js`，即每次上线JS，都会按时间给出地址
* 3、css、js，各自是一个域名，图片的话，有如下4个域名：
	* `http://i0.letvimg.com/`
	* `http://i1.letvimg.com/`
	* `http://i2.letvimg.com/`
	* `http://i3.letvimg.com/`
* 4、支持https、http无缝切换
* 5、负载力强，支持全球加速，再也不用担心JS挂掉了

#### 1、为毛都是单独的一级域名？
为了不与主站的域名重复，免得携带cookie过去

#### 2、为毛图片域名是4个，不是1个？
<!-- more -->
这个要提到“浏览器并发请求数”。
不同的浏览器，在http 1.0与http 1.1环境下，都是不一样的
像Firefox、chrome这类高级的浏览器，一般是4-8个，或者是6-8个，
像IE这种大哥，一般是2个，顶多4个
多个域名的话，就可以同步下载文件，加快图片的下载、展示速度

#### 3、图片域名是不是越多与好？
当然不是，不用的域名，得挨个去做DNS解析，多了的话，解析的越慢。
这里有个名词，`DNS预解析`，就是在头部写一堆如下的标签
``` html
<meta http-equiv="x-dns-prefetch-control" content="on" />
<link rel="dns-prefetch" href="http://i0.letvimg.com" />
<link rel="dns-prefetch" href="http://i1.letvimg.com" />
……
```
会提前对DNS进行解析，提高界面的渲染速度
