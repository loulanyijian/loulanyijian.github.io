---
title: X-Frame-Options 与 iframe嵌套
date: 2017-05-01 15:02:34
categories: [http]
tags: [http,response,iframe]
---

莫名其妙碰到一个bug，我们后台的一个界面，在我们外层界面使用iframe嵌套的话，该界面会显示空白，没发出任何请求，而单独打开该界面的话，立马正常显示。
抓包看之，结果该界面的响应头，多了一个`X-Frame-Options`头，值为`deny`
百度之，该响应有如下作用：

修改web服务器配置，添加`X-frame-options`响应头。赋值有如下三种：
* (1）`DENY`：不能被嵌入到任何iframe或frame中。
* (2）`SAMEORIGIN`：页面只能被本站页面嵌入到iframe或者frame中。
* (3）`ALLOW-FROM uri`：只能被嵌入到指定域名的框架中。

该参数可以有效防止界面被不法网站iframe嵌套，兼容性好，十分有效
恍然大悟，通知后台修改了一下。又学了一招。
