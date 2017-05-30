---
title: cookie详解
date: 2014-06-22 15:02:34
categories: [技术大杂烩]
tags: [cookie]
---



### 1. cookie是啥？能干啥？

##### 1.1 cookie是啥？

* 简单来说cookie就是通过客户端，存储的变量
* 一般情况下，服务端与JS都可以操作cookie，都可以对cookie进行写入与读取
	* 某些特殊情况下的cookie，JS操作不了

##### 1.2 能干啥？

* cookie可以做客户端缓存
* 进行网络请求时，cookie会自动挂在request header上，因此可以做用户登录状态的记录
	* 前端开发接口时，不用专门传输用户信息，cookie会自动带过去
	* 原生app请求接口时，不能主动携带cookie的，但是原生app，可以向H5界面种植cookie

### 2. cookie的属性列表

<!-- more -->

打开chrome的开发者工具，可以看到当前界面的cookie列表信息

<img src="https://loulanyijian.github.io/images/cookie.png" style="width:80%" alt="cookie列表信息">

##### Name
* cookie的存储方式类似于key-value形式，name可以理解为key
* 同域下，name不能重复，否则后者覆盖掉前面的
* 虽然允许中文存储，但是尽量不要使用中文存储，有的浏览器、有的场景下，会有兼容性问题，导致乱码，name尽量别是中文

##### Value
cookie的实际值，如果存储中文的话，需要进行编码，读取的时候再行解码

##### Domain

cookie所在的域，cookie不能跨域写入、读取，cookie默认存储在本域，也可以存储在本域的父级域名、根域之下

##### Path

* cookie存储的路径，如果不做特殊说明的话，cookie默认存储是当前路径，但是其余路径的界面，就无法读取到这个cookie
* 一般而言，都是存储到根目录，即/目录

##### Expires/Max-Age

为过期时间/最大时效
* 如果是显示未来的某个时间点，该条cookie会在这个时间点失效
* 如果是显示着为`session`或者/，证明该条cookie在浏览器关闭之后，就会时效

##### Size

cookie的大小，单位为字节，可以查看哪条cookie过去庞大，用于优化

##### HTTP

是否仅用于传输。如果该栏目为勾选状态，说明该条cookie是JS无法读取、写入的，只能通过服务器进行读写

##### Secure

是否仅适用于https，如果此项勾选，该条cookie仅在https下才能生效

##### SameSite

* 是否防止跨域发送。
* cookie信息是可以通过后台代码、node程序，post到服务器上去的，以通过验证，达到不可告人的目的。
* 如果改项为勾选，说明该cookie信息只能通过本域名下的请求才能传输，不能通过其他域名下发送

### 3. cookie的增、删、改、查-通过JS

服务端也可以对cookie进行同样的操作

##### 读取

document.cookie，即可获取当前域名全部可以JS操作的cookie信息，只是形式为字符串，没条数据按分号隔开，需要JS单独处理

##### 写入

`document.cookie="userId=828; userName=hulk; domian=demo.com; path=/; expire="+xxx;`

* 可以同时写入多条
* 必填项为  `key = value`
* domian 选填，默认为当前的域名，也可以设置当前域名的父级、根域名
* path 选填，默认为当前的路径，即`location.pathname`，一般设置为根目录 /
* expire 选填，默认是随着浏览器关闭即过期，如果填写的话，是未来的时间点

##### 改写

同样`document.cookie="userId=828; userName=hulk; domian=demo.com; path=/; expire="+xxx;`格式改写
只是path、domain，都需要与之前的统一，要不然不是改写之前的了，而是写入一个新的了

##### 删除

将cookie重新写入，过期时间为现在，或者现在之前的某个时间点即可

### 4. cookie与session

* cookie是客户端信息，session是服务端信息
* session在客户端中，通过cookie记录
* 非session的cookie不会随着浏览器关闭而消失，session会消失
* session过期，导致回话过期，网站重新登录等等
* session默认15分钟，可以通过Tomcat、Java项目等各种手段设置

### 5.cookie的注意点

* cookie是有限制的，不同的浏览器每个域名下，有不同的cookie条数限制，20-50条不等
* 浏览器一共可以存储4kb左右的cookie信息，多了的话就会删除旧的
* 由于cookie信息均会发送到服务器，多余的cookie的话，一是浪费带宽，二是增加请求成本，三是增加服务端解析成本
	* 所以cookie一定要减少体积，能不用的话就不用，以达到性能优化的目的
	* 静态资源文件，采用与主站不同的域名，避免在请求css、js的时候，携带上cookie信息

### 6. 扩展
* 原生操作cookie的话，还需要写一下公用JS代码，这里推荐一个JS操作cookie的代码示例。
[JS之——设置cookie 删除cookie - 刘亚壮的专栏 - 博客频道 - CSDN.NET](http://blog.csdn.net/l1028386804/article/details/51691035)

* 如果你用的是jquery做基础类库，这里还推荐一个[jquery cookie](https://github.com/carhartl/jquery-cookie)的插件库，基于jquery的，更是简单

### 7.总结

* cookie很好用，但是得谨慎
* 在浏览器全面兼容localstorage之前，cookie还是有很大用途的
* 预测在浏览器全面支持html5之后，cookie只会作为存储登录信息之用


