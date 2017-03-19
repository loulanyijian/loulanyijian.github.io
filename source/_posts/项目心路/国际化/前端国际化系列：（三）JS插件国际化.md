---
title: 前端国际化系列：（三）JS插件国际化
date: 2017-10-24 17:02:34
categories: 项目心路
tags: [国际化]
---

&nbsp;&nbsp;&nbsp;&nbsp;前面说了js的文案替换，使用`le-translate`把业务JS代码抽出了，还有我们使用的众多JS插件，各有自己的国际化方法，需要分别对待。

### 1、日期插件

&nbsp;&nbsp;&nbsp;&nbsp;日期插件，我们使用的有如下几种

#### 1、1 [`my97datepicker`](http://www.my97.net/index.asp)

&nbsp;&nbsp;&nbsp;&nbsp;作为老牌的JS日期选择器，my97以稳定、功能全面出名，最近更新时间为2013-12-16，可见有多么的自信。
&nbsp;&nbsp;&nbsp;&nbsp;97有自带的多语言功能，包括繁体中文、英文、简体中文，多传一个参数即可`onFocus="WdatePicker({lang:'en'})"`
<img src="http://localhost:4000/images/fanyi8.png" alt="my97datepicker英文版" style="width:50%">

#### 1、2 [`laydate`](http://www.layui.com/demo/laydate.html)

&nbsp;&nbsp;&nbsp;&nbsp;是一整套UI系统（[`layui`](http://www.layui.com/)）中的日期插件，不知为何之前有的业务线选择了这个插件，倒是不难看，不过不支持多语言。
&nbsp;&nbsp;&nbsp;&nbsp;没办法了，临时换插件，还需要再进行业务调试，也可能会影响整体UI，拿到laydate的源码，将里面的 `年`、`月`、`日`、`日期`、`日期不符合格式，请重新选择`等中文提示，都到JS最上面，做成字典表，又多接收一个调用参数，根据参数返回中文或英文。
&nbsp;&nbsp;&nbsp;&nbsp;注：laydate功能少不说，还有隐藏的bug，官网一直说要更新也没更新，我们后面的项目，果断抛弃了这个坑货。

#### 1、3 [`GRIcalendar`](http://down.admin5.com/demo/code_pop/19/789/)

&nbsp;&nbsp;&nbsp;&nbsp;是一个日期范围选择插件，开始日期与结束日期成对出现，十分好使，不过是个个人项目，也没有多语言配置，如处理laydate一样，手动修改一下源码就OK。
<img src="http://localhost:4000/images/fanyi9.png" alt="GRIcalendar英文改造版" style="width:50%">

### 2、在线编辑器

&nbsp;&nbsp;&nbsp;&nbsp;不同的产品线，使用了kindeditor与ueditor两种编辑器，所幸都是成熟产品，都有自己的国际化，多传参数即可。
<img src="http://localhost:4000/images/fanyi10.png" alt="ueditor英文版" style="width:70%">

### 3、验证插件
&nbsp;&nbsp;&nbsp;&nbsp;我们使用了`jQuery Validate`这个验证组件，本身就是英文版的，中文版反而是扩展的语言包，可以灵活展示。
``` javascript
messages: {
	required: "This field is required.",
	remote: "Please fix this field.",
	email: "Please enter a valid email address.",
	url: "Please enter a valid URL.",
	……
}
```

### 4、图表组件
&nbsp;&nbsp;&nbsp;&nbsp;图表我们使用了echart，普通的图表，如柱状图、折线图做国际化，只需将传入的X、Y轴坐标等配置信息修改成英文即可。
&nbsp;&nbsp;&nbsp;&nbsp;但是我们业务线还有国内流量、带宽、用户分布图，展示不同省份的分部情况，这样的话，需要将国内地图，修改成美国地图，展示美国不同州的统计情况。
&nbsp;&nbsp;&nbsp;&nbsp;直接按照echart的官网北美地图示例配置即可。
<img src="http://localhost:4000/images/fanyi11.png" alt="echart北美地图demo" style="width:70%">

### 5、其余不需要国际化的第三方插件
&nbsp;&nbsp;&nbsp;&nbsp;其余的很多第三方JS插件，例如上传使用的webuploader、优化单选多选框的icheck、模板引擎artTemplate、全屏插件fullpage.js、幻灯片插件swiper等等，无需要专门传入语言参数或修改源码，要么直接没有中文的元素，要么直接在使用的过程中，像修改业务JS代码一样，使用LCT()或翻译字典key-value形式做国际化处理。


### 6、自己开发的JS插件
&nbsp;&nbsp;&nbsp;&nbsp;我们项目组自己开发的JS插件众多，包括列表组件、分页组件、弹窗组件、下拉组件等，很多需要国际化的，这样的话，自己修改源码就好，思路如下：
* 1、找到JS插件中的所有中文
* 2、将找到的中文，抽到插件最上面，做成字典表
* 3、翻译字典表成英文字典表
* 4、将插件调用方法，多加一个语言参数配置，不传的话，默认文案走中文的，传的话，按传的参数进行展示

### 7、最后总结一句，是否自带国际化，是评价一个插件是否优秀的重要条件。


