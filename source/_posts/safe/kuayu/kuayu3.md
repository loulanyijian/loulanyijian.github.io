---
title: 跨域:（三）chrome浏览器本地跨域——Windows
date: 2016-08-06 15:02:34
categories: 跨域
tags: [跨域, chrome]
---

还有一种方法，可以在本地调试过程中，设置绕过跨域的问题。
这就是我们强大的chrome浏览器，有自己的方法。
### Windows chrome免跨域设置方式
在chrome的某个快捷方式下，右击选择属性，在属性页面中的目标输入框里加上   --disable-web-security  如下图所示：
<img src="http://www.spasvo.com/ckfinder/userfiles/images/2016030450158588.jpg?_=5544572" alt="" style="width:40%">
点击应用和确定后关闭属性页面，并打开chrome浏览器。如果浏览器出现提示“你使用的是不受支持的命令标记 `--disable-web-security`”，那么说明配置成功。
如上是旧版的chrome浏览器，如果是新版的话，就麻烦了点。

具体做法为：

* 1.在电脑上新建一个目录，例如：`C:\MyChromeDevUserData`

* 2.在属性页面中的目标输入框里加上   `--disable-web-security --user-data-dir=C:\MyChromeDevUserData`，`--user-data-dir`的值就是刚才新建的目录。

* 3.点击应用和确定后关闭属性页面，并打开chrome浏览器。

再次打开chrome，发现有“--disable-web-security”相关的提示，说明chrome又能正常跨域工作了。

![](http://images2015.cnblogs.com/blog/510823/201605/510823-20160531053346149-820598861.png)

**需要注意的是，如果使用跨域，必须通过该快捷方式打开，其余的地方打开的chrome，都不好使**

参考链接：
[chrome浏览器的跨域设置——包括版本49前后两种设置](http://www.cnblogs.com/laden666666/p/5544572.html)