---
title: 大前端接口规范
date: 2016-03-09 15:02:34
categories: 前端规范
tags: [规范,接口]
---

#### 1、基本规范
* 查询、获取之类的接口，通用get请求
* 添加、修改、删除的接口，通用post请求

#### 2、基本json格式
```javascript
	//当code == 200时候 是成功 data中是要用的数据
	//当code != 200时候 msg中是错误的信息，用于前端的错误提示
	{
	  "code": 200,
	  "data": {

	  },
	  "msg": "xxxxxxxxxxx",
	}
```

<!-- more -->

* 通过code判断接口成功与失败与否，失败的话，前端直接展示msg返回的内容，具体内容后端输出
* 不能通过返回的msg进行判断，msg只是用于直接获取在前端界面展示的文案

#### 3、key值
* 如果列表接口中没有的数据，也需要将json的key返回，不能缺少key值，
* 默认的key－value
* json：｛｝
* array：［］
* string：''
* number：0

#### 4、语义化
* 接口名称语义化，以动词+名词组合，例如getVideoList、editVideoInfo 
* 不接受list.html格式的接口，会误认为是静态界面 
* 接口字段语义化，符合大众阅读标准

#### 5、时间格式
* 传入、传出时间，都按标13位准时间戳来显示
* 不接受各后端不同的类似于2016-11-12 12：00：00这种返回

#### 6、关于跨域
* 如果有跨域请求的接口，需要加上jsonp格式的调用
* 据现有多数的接口，callback的key值为jsoncallback，
* 如果接口为不同的key值的话，预先通知到前端

#### 7、编码
* 请求、返回的编码，均必须为utf-8编码，不允许出现返回乱码，乱码不利于抓包调试
* 由于ie系的bug，接口请求的时候，需要把请求中的中文字段编码，后台接口请解码控制

#### 8、体积
* 接口尽量体积小，没必要将字段删减到最小，但最好不要上100k

#### 9、分页格式
* 请求接口，当前页码key——page
	* 以1开始
* 每页条数key－rows
	* 一般是10
返回格式
```javascript
{
  "code": 200,
  "data": {
    items:[
        {
            "id":1,
            "name":"xxx"
        },
        {
            "id":2,
            "name":"xxx"
        }
    ],
    "page": {
        "curPage": 1,
        "pageSize": 10,
        "totalPage": 2,
        "totalRow": 20
    }
  },
  "msg": "xxxxxxxxxx",
}
```
#### 10、添加回调
* 默认需要将新添加的json对象返回，用于不刷新界面继续操作
#### 11、session过期
* 后台返回接口
``` javascript
ajax: httpstatus 400
{
	"errCode":"9000",
	"errMsg":"http://uc.lecloud.com/login.do?backUrl=http://saas.lecloud.com",
	"errShowMsg":"用户未登录"
}
```
* 前台控制—jquery ajax统一过滤
``` javascript
//判断控制浏览器跳转，http code为400时，判断errcode值
$(document).ajaxError(function(event,request,settings,thrownError){
    console.log(request);
    try{
        if(request.status == 400){
        var responseJSON = JSON.parse(request.responseText);
        if(responseJSON.errCode == 90000){
            top.window.location.href = responseJSON.errMsg;
        }
    }
    }catch(e){}
});
```
#### 12、分享、同步策略
* 具体接口由后端的同学在开发之前，写在自己项目的wiki上面
* wiki上接口文档，如果返回的内容
* 接口变动的话，通知到前端同学
* 如果是多终端公用的接口，wiki上面使用者将自己的使用情况备注一下
* 各后端系统尽量保持一致，开发之前，前后端确认接口
* 如果是提供给多端的接口，格式化的内容尽量在后台接口中统一，以达到各终端显示一致
