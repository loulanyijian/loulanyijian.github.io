---
title: localStorage 做性能优化
date: 2014-11-12 15:02:34
categories: html5
tags: [html5,localStorage,性能]
---

localStorage作为cookie的替代品，可以对前端性能优化做一些文章。

### 缓存普通数据

由于不会被http请求带上，localStorage本事对性能就算优化了一层

### 缓存接口

这个业内使用的也比较多，对那些请求量比较大、而且改动不算频繁的接口，可以通过localStorage缓存到本地

大体思路：
* 第一次请求接口时，正常请求并存入localStorage，同时存入当前时间戳
* 再次使用该接口时，对比当前时间与存入的时间戳，如果未到存储时间的话，直接从缓存中取数据
* 如果时间超时，再次正常请求接口，并更新时间、接口内容到缓存

下面是我封装了一个`getLocalOrRemote.js`

<!-- more -->

``` javascript
/**
 * [getLocalOrRemote 获取本地或者远程数据]
 * @param  {[type]}  localstorage key      [description]
 * @param  {[type]}   time     [时间戳，以秒为单位]
 * @param  {[type]}   url      [远程获取的url，要全]
 * @param  {Function} callback [回调的方法]
 * @return {[type]}            [description]
 */

// 工具类
function getLocalOrRemote(key, time, url, callback) {
    var nowTimes = (new Date()).valueOf();
    var localObj = {},
        realObj = {},
        localTimes;

    // 如果存有本地缓存的话
    if (localstorage[key]) {
        localObj = JSON.parse(localstorage[key]);
        localTimes = localObj.lcTime;
        // 如果没过期的话，取本地数据
        if ((nowTimes - localTimes) / 1000 < time) {
            getDataFromLocal();
        } else {
            getDataFromRemote();
        }
    } else {
        getDataFromRemote();
    }

    function getDataFromRemote() {
        $.ajax({
            type: "GET",
            url: url,
            dataType: "jsonp",
            success: function(data) {
                nowTimes = (new Date()).valueOf();
                var localObjNew = {};
                localObjNew.lcData = data;
                localObjNew.lcTime = nowTimes;
                localstorage[key] = JSON.stringify(localObjNew);

                callback(data);
            }
        });
    }

    function getDataFromLocal() {
        var data = JSON.parse(localstorage[key]);
        realObj = data.lcData;
        callback(realObj);
    }
}

// 使用demo
var url = 'xxx';
getLocalOrRemote("aiJia", 300, url , function(data) {
    // 拿到data执行业务逻辑……
});

```

### 缓存css、js文件

类似于缓存接口，可以在第一次请求到css、js文件之后，缓存到localStorage里面，下次如果命中缓存的话，通过appendChild的方法，塞到界面的head中。
这种缓存意义比较小，因为css、js文件，一般非首次请求的话，就会命中缓存，最少也是协商缓存，即http为304的请求。
如果使用cdn的话，会命中强缓存，压根不用执行JS文件去判断是否到期，直接通过浏览器的内部缓存机制，直接从缓存里面拿数据，省事的很。

### 缓存图片

localStorage只能缓存字符串，但是可以通过与canvas配合，将图片缓存起来

``` javascript
 // 图片加载完成后执行，通过canvas将图片转为base64，存入缓存
 
 a.addEventListener("load", function () {

 var imgCanvas = document.createElement("canvas");
 imgContext = imgCanvas.getContext("2d");
// 确保canvas尺寸和图片一致
 imgCanvas.width = a.width;
 imgCanvas.height = a.height;
// 在canvas中绘制图片
 imgContext.drawImage(a, 0, 0, a.width, a.height);

// 将图片保存为Data URI
 gsFiles.a = imgCanvas.toDataURL("bj.png");

gsFiles.date = todaysDate;

// 将JSON保存到本地存储中
try {
localStorage.setItem("gsFiles", JSON.stringify(gsFiles));

}
catch (e) {
console.log("Storage failed: " + e);
}
}, false);


// 取到缓存里面的数据，还原到图片地址上
// Use image from localStorage
a.setAttribute("src", gsFiles.a); 
```

### 总结

localStorage可以缓存N多东西，但是在开发、管理缓存上，也需要多花一些精力，具体还需要看业务需求。






