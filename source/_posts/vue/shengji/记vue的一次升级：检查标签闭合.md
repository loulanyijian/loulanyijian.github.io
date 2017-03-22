---
title: 记vue的一次升级：检查标签闭合
date: 2017-03-21 17:02:34
categories: [vue实践]
tags: [vue]
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;前段时间开发了vue的组件库——`liveUI`，供团队内部使用，自己写了N个组件，剩余的打算让项目组老郑、阿旭来完善，大家一起写代码。
&nbsp;&nbsp;&nbsp;&nbsp;阿旭最近有时间了，git上拉了代码， 一跑，报错了，提示标签未闭合。
&nbsp;&nbsp;&nbsp;&nbsp;怪了，一个月前我开发的时候，好好的，估计是因为vue升级的原因。

&nbsp;&nbsp;&nbsp;&nbsp;问了一下老郑，他前两天也拉过这个组件库的代码，完善过组件。果然，<!--more-->他前两天拉代码的时候，也报错了，fix了N个未闭合的`html tag`，就好了。
&nbsp;&nbsp;&nbsp;&nbsp;想起来了，前两天，是看尤大说vue升级了一个中级版本，vue由`v2.1.x`升级到了`v2.2.0`，当时扫了几眼，感觉跟自己没关系，现在又仔细看了一下，果然，严格检查了未闭合的标签，遇到错误就直接抛错误了。
&nbsp;&nbsp;&nbsp;&nbsp;好吧，都怪自己不严格追随尤大，好好研究了一下其余的更新log，其余的影响不是很大，未到改变之前项目代码的程度，默默的在心里注意一下就行了。
&nbsp;&nbsp;&nbsp;&nbsp;vue与react越来越像了，前段时间，开发react的时候，一大段html段落，制作成vue的`template`时，正常运行，通过react的jsx语法时，就会报标签未闭合，当时还好好嘲笑了一把react，认为它不健壮，现在看来，都一样了。