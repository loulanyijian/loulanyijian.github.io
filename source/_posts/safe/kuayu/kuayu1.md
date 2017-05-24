---
title: 跨域:（一）接口跨域
date: 2015-09-04 15:02:34
categories: 跨域
tags: [跨域, iframe, jsonp, reponse]
---
鄙人自封公司第一跨域解决大师，的确需要写一下关于跨域的事情。

前端调试，跨域太常见了。如下图：
![chrome下跨域提示](https://loulanyijian.github.io/images/kuayu1.png)
跨域的原因，是浏览器的安全机制，不允许跨域互相调用，会提高网站的安全性。

前端跨域的最大模块，是ajax接口跨域

### 1、最简单的解决方法：jsonp
虽然jquery将jsonp封装到了ajax方法里面，但是底层的代码调用，完全不是一样。
jsonp的原理，就是通过script标签进行回调，原生的jsonp开发，会明显一些。
``` javascript
// 定义好回调方法
function qqq(data){
// do something
}

<script scr='http://xxx.com?callback=qqq'></script>>
```
也就是相当于，服务端返回的代码，使用了qqq包了起来，然后调用了上面定义的那个qqq方法，实现了数据的跨域调用。

#### 使用jsonp的注意点
* 需要与后台定义回调key值
	jquery的默认回调key值，是callback，但是有的后台，为了数据的隐私性，会设置一个特殊的回调key值。
	这样的话，需要单独在jquery ajax里面，设置回调key值
	`jsonp: callback2`
	然后发出的请求，就是`http://xxx.com?callback2=qqq`，
	如果不设置，或者设置的不对的话，请求会报错。

* jsonp的缺陷
	* 只支持get方式
		因为是动态创建script。
		关于安全性要求比较高、数据量比较大的接口，就不太好了
	* 不支持同步
		只能是异步的。
		如果是需要获取到验证信息，并同时阻断其余操作的接口的话，无法进行。

* 可以支持缓存
	jquery创建jsonp的话，callback的value值，默认会添加一大堆，防止缓存。
	其实也可以支持callback的value值固定，来配合运维同事做接口缓存。
	`callback: qqq`

* 类库支持
	jquery、zepto都支持jsonp，vue之前推荐的ajax库：`vue-resource`，也支持jsonp。
	但是vue官方最近推荐的ajax库——`axios`，不支持jsonp。

### 2、最省事的解决方法：后端设置跨域response头
服务器端对于CORS的支持，主要就是通过设置`Access-Control-Allow-Origin`来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。
不同的后端语言，Java、PHP，都会有自己的设置方法，简单的很。
前端调试的时候，只需要抓包看这个接口的response header中，是否有`Access-Control-Allow-Origin`属性。

* cookie的附加
跨域请求，默认是不带上cookie信息的，因为不是一个域了，cookie也有自己的域，要不然就乱了。
但是很多情况下，我们是需要带上cookie信息的，这时候我们伟大的后端，需要多添加一个参数
`Access-Control-Allow-Credentials:true`
然后将前面的`Access-Control-Allow-Origin`，改成具体的域名，这个是浏览器的另外一个安全要求，即不能使安全性过低，会有隐患。

然后前端在ajax的时候，需要进行单独设置：
``` javascript
crossDomain: true,
withCredentials: true
```
### 3、在小范围很有效的解决方案：document.domain

这个仅适用于跟域名相同的跨域，如`a.lecloud.com`，与`b.lecloud.com`，如果不做处理的话，这俩是跨域的。
如果这俩域名下的JS文件，都做了`document.domain = 'lecloud.com'`，两者就不会跨域了，省了使用jsonp、响应头设置了。
如果不特殊处理的话，`document.domain`的值是该域的完整域名。
该方案有隐患，之前遇到过的，使用了`kindeditor`，里面的上传图片，会创建一个iframe，用于上传，该iframe使用了父域名的domain，然后我又改写了父域名的domain，造成了跨域。

### 4、双层iframe调用
这个一般适用于使用第三方登录、或者第三方什么的跨域调用，思路比较巧妙。

例如：
我们乐视云的官网，使用了乐视网的第三方登录：
www.lecloud.com，嵌套了www.le.com的iframe，登录成功之后，www.le.com动态创建一个www.lecloud.com的iframe，并将值通过src传入。
* 第一层：www.lecloud.com
	* 第二层：www.le.com
		* 第三层：www.lecloud.com

孙子层的iframe与第一层（爷爷层）的主页面，是同域的，可以进行数据的传输与方法的调用，通过`parent.parent.xxx()`调用，就OK鸟。
这个一般利用情景比较少，一般自己公司开发的话，没有这么麻烦的调用方式。

### 5、后端做代理
如果我们请求一个其余网站的接口，无法进行跨域，可以通过后端同学，通过后端代码进行数据的拉取、透传，然后与前端同域调用。

### 6、html5的postMessage
这个鸟玩意，还没开始，就已经没人用了



