---
title: Firefox JS兼容性问题
date: 2016-07-06 15:02:34
categories: 兼容性
tags: [兼容性,Firefox]
---

* 拖拽bug
* 数组sort排序

强大如`Firefox`，也会有兼容性问题。
### 1、拖拽的bug
使用了诸如`sortable.js`等拖拽插件，拖拽完成之后，会自动打开新网页，打开百度搜索，搜索当前的选中的dom。
解决方案：
* 要么换拖拽插件
* 要么`Firefox`提示，`请按照提示修改浏览器配置……`
<!--more-->

### 2、数组排序
如下代码：
``` javascript
var a = [1,3,2];
a = a.sort(a)
```
在`chrome`下，会输出`[1, 2, 3]`
在`Firefox`下，会报`TypeError: wrappedCompareFn is not a function`错误。
意思为应该传`function`的参数，传了个非`function`参数。
解决方案：定义个`sort function`，传入进去。

### 3、其余
其余的`event`、dom操作的异常，早已经熟悉了，通过jquery或者vue等类库，可以解决。
Firefox还算OK，有对网站的分析，但是调试费劲，还是不如chrome的好。