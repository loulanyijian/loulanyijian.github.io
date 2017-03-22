---
title: vue1.0升级2.0
date: 2016-10-09 15:02:34
categories: [vue实践]
tags: [vue]
---

&nbsp;&nbsp;&nbsp;&nbsp;国庆佳节，尤大发布了vue2.0的正式版，让人不好好过节啊。
&nbsp;&nbsp;&nbsp;&nbsp;节日回来后，虽然vue官网上的教程还是1.0版本，但2.0是趋势，而且我们使用vue的项目还在开发阶段，现在上车，还来得及。
&nbsp;&nbsp;&nbsp;&nbsp;作为我们使用的第一个正式vue项目，有点试水的感觉，未使用`vue-router`，所以，只涉及vue核心语法的升级。
&nbsp;&nbsp;&nbsp;&nbsp;针对项目的实际情况，现总结如下：

<!--more-->

### 1、双大括号-`Mustache语法`使用的限制
&nbsp;&nbsp;&nbsp;&nbsp;之前vue1.0最灵活的地方，就是双大括号使用的灵活，之前是支持这种写法的
``` javascript
<a href="xxx.com/id={{id}}">{{id}}</a>
```
&nbsp;&nbsp;&nbsp;&nbsp;升级之后，属性中已经不支持双大括号了，只能写成`v-bind`了，如下：
``` javascript
<a :href="'xxx.com/id='+id">{{id}}</a>
```

### 2、取消了三大括号
&nbsp;&nbsp;&nbsp;&nbsp;1.0的时候，渲染html片段，可以直接使用三大括号来嵌套，如下：
``` javascript
<!--domString是从后台拿到的带标签的dom结构-->
<div>
	{{{domString}}}
</div>
```
&nbsp;&nbsp;&nbsp;&nbsp;升级后，需要使用`v-html`替代了
``` javascript
<div v-html='domString'></div>
```
&nbsp;&nbsp;&nbsp;&nbsp;效果是一样的

### 3、生命周期钩子的改变
&nbsp;&nbsp;&nbsp;&nbsp;个人感觉尤大有点借鉴react的意思，改变了之前好好的生命周期，统统换了个名字，需要适应一下。

### 4、过滤器的限制
&nbsp;&nbsp;&nbsp;&nbsp;这么好使的过滤器，一下子变得不好使了。之前我们的一个后端架构师做个人项目时，就因为vue自带的过滤器缺乏，选择了去哪儿网的[avalon](http://avalonjs.coding.me/)。
&nbsp;&nbsp;&nbsp;&nbsp;过滤器现在只支持插入文本之内的格式，不再支持属性、方法内的过滤器了。
&nbsp;&nbsp;&nbsp;&nbsp;这个很郁闷，因为我们过滤器的使用十分多，总结了一下，有如下几个替换方法：

* 1、简单的逻辑操作，直接写JS行内表达式来处理
* 2、复杂的、不需要循环的逻辑，使用计算属性来代替
* 3、复杂的、需要循环的逻辑，使用`method`里面的方法来处理

&nbsp;&nbsp;&nbsp;&nbsp;过滤器使用的参数，也跟之前不一样了，参数需要通过括号包起来了

### 5、不能绑定到body或者html上面了
&nbsp;&nbsp;&nbsp;&nbsp;这个好说

### 6、v-for的改变
&nbsp;&nbsp;&nbsp;&nbsp;之前内置的`$index`去除了，需要自己显式的去定义
&nbsp;&nbsp;&nbsp;&nbsp;下标从1开始了，这个让我费解，不都是从0开始么？

### 7、v-for key的使用
&nbsp;&nbsp;&nbsp;&nbsp;我们项目中有拖拽的功能，之前很好实现，拖拽完成之后，回调方法处理dom列表绑定的数据列表，把数组的旧下标i与新下标j替换一下即可。
&nbsp;&nbsp;&nbsp;&nbsp;现在不行了，调试的时候发行，数组是替换过来了，但是dom列表又还原了，没被拖拽！
&nbsp;&nbsp;&nbsp;&nbsp;先后去了`sortable.js`的github，又去了vue 的github，在vue的`issue`发现了有人提过这个问题，尤大回复的是要将key加上，不同的值来区分不同的dom。
&nbsp;&nbsp;&nbsp;&nbsp;试了一下，果然可以！
&nbsp;&nbsp;&nbsp;&nbsp;因为vue现在使用了虚拟dom，对必要的dom操作，还是要有一些限制的。

### 8、总结
&nbsp;&nbsp;&nbsp;&nbsp;按上面的修改，再处理其余小的升级细节，我们的项目就支持vue2.0了，有了vue官网的帮忙，升级的还算比较利索。
&nbsp;&nbsp;&nbsp;&nbsp;vue还去除了对dom的操作，这个我举双手赞成，有了vue，就需要使用数据来操作dom，退一万步讲，就算要亲自操作dom，也不需要vue来操作。
&nbsp;&nbsp;&nbsp;&nbsp;整理来说，vue1.0升2.0还是很有意义的，虽然我对过滤器使用的限制十分不爽，但是引入了虚拟dom这个杀手锏，优化了其余的组件部分，vue时候要挑战JS圈了！




