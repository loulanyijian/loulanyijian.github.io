---
title: 从vue打包文件看项目JS引用
date: 2017-01-16 15:02:34
categories: 性能优化
tags: [vue,性能]
---

&nbsp;&nbsp;&nbsp;&nbsp;使用`vue-cli`开发`vue web app`，首先考虑的是线上环境的打包部署，一开始以为无论多少个界面，只会打出一个超级大的JS，首次请求的时候巨慢无比。
&nbsp;&nbsp;&nbsp;&nbsp;后来发现我错了，vue可以借助`webpack`，N个界面，可以打出对应的N个JS，按需加载。
&nbsp;&nbsp;&nbsp;&nbsp;这个好，符合我的性能观点，按需加载。
&nbsp;&nbsp;&nbsp;&nbsp;运行`npm run build`进行打包，会打出`N+3`个JS文件，如下图：
<!--more-->
<img src="https://loulanyijian.github.io/images/vue-file.png" alt="打包结果" style="width:30%">
&nbsp;&nbsp;&nbsp;&nbsp;上图的`0-2`，是指我这个项目，共有3个路由界面，对应的3个业务js
* app.js，是我们项目的公用JS代码，入口就是`main.js`，这个公用代码，就是指除了在`node_moudles`公用包之外的公用代码。

&nbsp;&nbsp;&nbsp;&nbsp;打出的另外两个JS，分别是`vendor.js`、`manifest.js`

* `vendor.js`是从`node_modules`包中提取的公用的JS代码库，与`app.js`不同，这个里面无业务JS。
* `manifest.js`是个索引文件，不同的界面，通过`manifest.js`文件，调用上面`0-2`的业务JS。

&nbsp;&nbsp;&nbsp;&nbsp;这个跟我们之前的生产环境JS部署很类似
&nbsp;&nbsp;&nbsp;&nbsp;乐视网最早之前的JS部署，每个界面如下:
``` html
<script src='abc.js'></script>
<script>
	__loadjs('list')
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;`abc.js`，是一个索引文件，代码如下：

``` javascript
(function(window){
	var ver = {
		"list":"04_js/2017**/15/17/14"
		"index":"01_js/2017**/15/17/14"
		 ……
	};

	//读取入口文件
	window.__loadjs = function(js){
		document.write('<script type="text/javascript" src="//js.letvcdn.com/lc'+(ver[js]||local)+'.js"></script>');
	};
})(window);
```
&nbsp;&nbsp;&nbsp;&nbsp;`__loadjs`根据传入的字符串，同步加载cdn上的JS。

&nbsp;&nbsp;&nbsp;&nbsp;后来我觉得这个的话，每个界面的JS都不一致，像`jquery`那种大而且公用的代码，都被打到不同的JS里面，无法做缓存。
``` html
<script src='header.js'></script>
<script src='abc.js'></script>
<script>
	__loadjs('list')
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;如上是我改进后的，多了一个`header.js`，里面存了一些公用的JS，包括`jquery`、`ajax url`配置、常用工具类等JS，`__loadjs`，只加载自己界面的业务JS。
&nbsp;&nbsp;&nbsp;&nbsp;这样的好处，是将一个比较大的`header.js`，在请求完一次，都304缓存起来，减少了请求
&nbsp;&nbsp;&nbsp;&nbsp;由此看来，

* `abc.js` = `manifest.js ` 
* `header.js` = `vendor.js+app.js`

&nbsp;&nbsp;&nbsp;&nbsp;异曲同工之妙啊！



