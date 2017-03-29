---
title: vue开发规范
date: 2017-01-15 15:02:34
categories: [vue实践]
tags: [vue,规范]
---

### 0. 遵循的大JS规范
&nbsp;&nbsp;&nbsp;&nbsp;遵循`Airbnb`的`eslint`规范

### 1. 版本选择

* 选择`vue2.0`最新版本进行开发
* js版本，选择`es6、7`进行开发，只要`babel`支持转义就OK

### 2. 语法规范
* 无特殊说明的话，vue的命名、缩进，与JS的命名规范一致，遵循`Airbnb`的`eslint`规范
<!--more-->

#### 2.1 vm对象
&nbsp;&nbsp;&nbsp;&nbsp;实例化的vm对象，统统以`*Vue`来命名，如主界面的vue对象，使用`mainVue`

#### 2.2 传参的回车方式
&nbsp;&nbsp;&nbsp;&nbsp;一个参数一个回车，前面对齐
``` javascript
// bad
<li v-for="item in templateList"
  @click="chooseModal(item.id,item.activityTypeId)" @mouseenter="mouseoverFun(item.id)" @mouseleave="mouseoutFun">

// good 
<li 
    v-for="item in templateList"
    @click="chooseModal(item.id,item.activityTypeId)" 
    @mouseenter="mouseoverFun(item.id)" 
    @mouseleave="mouseoutFun">
```

### 3. 公用部分

#### 3.1 过滤器编写

&nbsp;&nbsp;&nbsp;&nbsp;通用的过滤器方法，如日期、图片等，写到公用的`commonFilter.js`方法里面，全局引用
&nbsp;&nbsp;&nbsp;&nbsp;单个使用的过滤器方法，放到单独的业务代码之中

#### 3.2 指令编写

&nbsp;&nbsp;&nbsp;&nbsp;类似于过滤器，必要的话，提出公共的来

#### 3.3 static文件夹
&nbsp;&nbsp;&nbsp;&nbsp;该文件夹只放不能被webpack处理的css与JS文件，如`baseCore.css`、`modify.css`
&nbsp;&nbsp;&nbsp;&nbsp;其余的类似`config.js`，需要放到src下面，被webpack处理

#### 3.4 `svg split`
&nbsp;&nbsp;&nbsp;&nbsp;公用的一大堆svg元素，不能直接写到`index.html`中，需要处理到单独组件中，保证`index.html`干净

### 4.插件选择
&nbsp;&nbsp;&nbsp;&nbsp;vue自带的靠谱插件，`vue router`、`vuex`、`vue resource`，其余的，呵呵

#### 4.1 日期插件

&nbsp;&nbsp;&nbsp;&nbsp;选择`my97date`，这个可以做双向数据绑定
&nbsp;&nbsp;&nbsp;&nbsp;千万不能使用`laydate`，有bug，扩展性也不行

#### 4.2 ajax插件

&nbsp;&nbsp;&nbsp;&nbsp;vue官方推荐axois，但是这个不支持jsonp，可以使用`vue resource`来支持jsonp

#### 4.3 radio美化插件

&nbsp;&nbsp;&nbsp;&nbsp;自写样式，替代`icheck`插件，实现双向数据绑定

### 5. 单文件组件

* 三大模块顺序 `template`——`script`——`style`，顺序放置
* 模块直接，保留一个空行
* 自定义的模块，要放到最后
* style，要添加`scoped`，如果是多处用到的样式，写到`modify.css`里面
* script里面代码顺序
	* import
	* export
		* name
		* mixins
		* components
		* props
		* data
		* computed
		* watch
		* method
		* 周期钩子
			* 按周期调用

### 6. 其余的待观察总结

