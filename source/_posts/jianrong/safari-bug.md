---
title: safari的兼容性问题
date: 2017-02-24 15:02:34
categories: 兼容性
tags: [兼容性,safari]
---

&nbsp;&nbsp;&nbsp;&nbsp;想不到，Safari这么先进的浏览器，也会有兼容性问题。
### 1、`new Date()`的限制
&nbsp;&nbsp;&nbsp;&nbsp;日期选择器，选择了诸如`s = '2017-02-24 12:00'`格式的日期，然后再`new Date(s)`
&nbsp;&nbsp;&nbsp;&nbsp;再看s，就是`Invalid Date`，非法日期
<!--more-->
``` shell
> var d = new Date('2017-02-24 12:00')
< undefined
> d
< Invalid Date = $1
```
&nbsp;&nbsp;&nbsp;&nbsp;这个在chrome与Firefox下，是可以的。Safari下面，可以`new Date('2017-02-24')`，不能再有附加的格式了

&nbsp;&nbsp;&nbsp;&nbsp;解决方案：使用正则处理。

### 2、css3兼容性
&nbsp;&nbsp;&nbsp;&nbsp;有点记不得了，去年开发了一个闪烁的提示框，别的浏览器，包括IE11，都好好的，在Safari下面，会闪烁错乱，当时是按优雅降级处理的。

### 总结：
&nbsp;&nbsp;&nbsp;&nbsp;Safari是基于webkit内核的，做的的确还不错，兼容性问题不多。
