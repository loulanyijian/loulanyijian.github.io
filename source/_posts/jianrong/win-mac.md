---
title: window与Mac系统兼容性问题
date: 2017-05-15 15:02:34
categories: 兼容性
tags: [兼容性,mac]
---

为了工作方便，最近封装了一个npm包上传的公网上去了，在项目中引用，用的时候还算好使。
项目提测的时候，产品经理说有界面有问题，检查了之后发现，那个npm报错了。
产品经理使用的是window版本的chrome，我们几个开发的，使用的是Mac版本的chrome。
原来在不同系统之间的同类型浏览器，也有兼容性问题。
类似的，还有Windows、Linux与Mac版本的Firefox、Windows与Mac版本的Safari
不过好在应当问题不多，写代码的时候需要注意，少用一些奇技淫巧……