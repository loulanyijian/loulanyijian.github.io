---
title: 大前端JS书写规范——airbnb规范
date: 2017-03-28 15:02:34
categories: 前端规范
tags: [规范,eslint]
---

&nbsp;&nbsp;&nbsp;&nbsp;之前是使用jshint做的代码检测，只是在sublime中加上了提示，后来开始做vue的时候，尝试了一下eslint，觉得限制太多，无法写代码了。
&nbsp;&nbsp;&nbsp;&nbsp;最近由看小组其余成员写的代码，有的惨不忍睹，有的千奇百怪……认识到，还是使用eslint的好。

&nbsp;&nbsp;&nbsp;&nbsp;今天使用`vue-cli`新建vue项目的时候，选择使用`eslint`的时候，发现多了一个步骤，就是可以选择代码风格的标准。
&nbsp;&nbsp;&nbsp;&nbsp;第一种是标准的，第二种是`Airbnb`的，第三种是完全自己添加的。
&nbsp;&nbsp;&nbsp;&nbsp;`Airbnb`的之前没用过，于是搜索之，别说，规范还真挺全，中文版也有。
<!--more-->

&nbsp;&nbsp;&nbsp;&nbsp;详细版地址：
&nbsp;&nbsp;&nbsp;&nbsp;[https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)
&nbsp;&nbsp;&nbsp;&nbsp;[中文翻译版](https://github.com/yuche/javascript)

&nbsp;&nbsp;&nbsp;&nbsp;现将主要的与`Standard`不同的地方说一下；
* 1、默认必须要分号，而eslint默认不添加分号
* 2、默认不允许使用var创建变量，而是使用let 或 const代替
* 3、接上一条，如果使用了let创建了变量，在后面没有对此变量改变，应当使用const代替
* 4、最变态的一点，不能使用for循环
    就算是设置了可以使用for循环，不能`for(let i = 0;)`，会提示要使用const代替
* 5、对箭头函数的使用
    能使用监听函数的，需要使用监听函数
    对箭头函数使用的限制，有很多。
* 6、空格的不同
  定义属性时，如 `a : 1`，在`eslint`的标准版，冒号前后需要都加空格，而在`airbnb`中，冒号前面不能加空格。

* 7、还有一些更严格的语法，待观察

&nbsp;&nbsp;&nbsp;&nbsp;**刚好我们现在要开始一个新的vue webapp开发，刚好，从这个系统开始，强推一下JS规范，顺便把ES6的语法强化一下，虽然开始的时候肯定会阵痛，但我相信是值得的**