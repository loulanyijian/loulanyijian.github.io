---
title: localStorage以及与cookie对比
date: 2014-11-11 15:02:34
categories: html5
tags: [html5,localStorage,cookie]
---

最近做一个项目，可以只兼容现代的浏览器，客户端存储就使用了localStorage。

localStorage与sessionStorage作为客户端存储数据的手段，是cookie这方面的替代品，与cookie相比，localStorage有明显的优点。

### cookie vs localStorage

<!-- more -->

* cookie存储有限，浏览器最多存4k；localStorage浏览器可以存5M
* cookie同域名下50个置顶（最新浏览器可能多些了）；localStorage存储，无域名限制
* cookie都会随着网络请求，传输到服务器，一定情况下，会造成性能浪费；localStorage不会传输
* cookie可以设置过期时间，或者浏览器关闭即过期；localStorage永不过期，只能通过JS删除
* cookie可以设置根域名；localStorage只能是当前的域名，无法更改，而且取不到其余域下的
* cookie可以设置path路径，用于做数据隔离；localStorage没有path，只能存储在根路径下
* localStorage使用JS操作的代码，比cookie操作的代码简单的多，因为它只有key-value这俩字段

### localStorage VS sessionStorage

两者只有一个区别，就是sessionStorage在浏览器关闭的时候，会消失掉，而localStorage不会消失掉
浏览器刷新界面的话，sessionStorage也不会消失

### localStorage的限制

* localStorage只能存储字符串类型的数据，如果是int、float数据，可以直接存储，拿出来的时候，需要进行转换
* 如果是数组、json数据的话，需要先通过`JSON.stringify`将数据处理成字符串存入，取出来的时候，需要通过`JSON.parse`将数据还原成之前的格式
* 兼容性，IE8及以下破浏览器不支持，这个慢慢可以忽略了
* localStorage的读取需要浏览器IO操作，也不是越多越好
* 在浏览器的隐私模式下，localStorage是不好使的
* 在IOS的隐私模式下，通过`window.localStorage`判断，localStorage是好使的，但是实际上，数据会存入不上

### 总结

localStorage的出现，为浏览器端数据缓存，推进了强大的一步