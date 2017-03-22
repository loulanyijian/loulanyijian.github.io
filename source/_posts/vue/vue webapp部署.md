---
title: vue webapp部署规范
date: 2017-03-14 15:02:34
categories: [vue实践]
tags: [vue,nginx]
---

&nbsp;&nbsp;&nbsp;&nbsp;最近小组多个vue的web app项目进入部署阶段，跟不同的后端沟通如何部署我们前端工程的事情，又是说了N遍，决定还是记录一下，以后拿文档怼他们。
&nbsp;&nbsp;&nbsp;&nbsp;首先，要明确我们前端开发的是[spa单界面应用](http://baike.baidu.com/item/SPA/17536313#viewPageContent)，不管多少界面，我们只会部署一个很小的`index.html`文件，具体路径，都通过前端路由来分发，所有的逻辑，都会写到js里面，包括以后的文案修改。

### 1、与本项目后台接口域名一致，路径为`portal`
<!--more-->

&nbsp;&nbsp;&nbsp;&nbsp;如当前项目接口为 `http://xxx.lecloud.com`，那前端部署后的请求地址，应当为 `http://xxx.lecloud.com/portal`，进入我们自己的index.html文件，来做路由分发。
&nbsp;&nbsp;&nbsp;&nbsp;既免去了调试跨域的麻烦，又不会与后台的接口混淆。
&nbsp;&nbsp;&nbsp;&nbsp;需要在`vue-router`设置的地方，做如下设置，要不然界面请求不到JS：
``` javascript
const router = new VueRouter({
  mode: 'history',
  base: 'portal',// 前端部署路径
  ……
```

### 2、配置nginx
&nbsp;&nbsp;&nbsp;&nbsp;为了使地址看起来顺眼，`vue-router`需要设置成`history`方式（如上面代码展示）。
&nbsp;&nbsp;&nbsp;&nbsp;这样的话，请求的实际上是虚拟的地址，需要后台设置nginx支持，思想就是将所有`http://xxx.lecloud.com/portal/xx/yy`等前端目录下的请求，统统打到前端的`index.html`文件上，来做路由分发。
&nbsp;&nbsp;&nbsp;&nbsp;nginx配置如下：
``` conf
……
location ^~ /portal {
    #alias  /***/www/****-webapp/portal/;
    rewrite ^/portal/(.*)$ /index.html break;
}
……
```

### 3、使用火星一号部署，前后端分离
&nbsp;&nbsp;&nbsp;&nbsp;火星一号是我们公司开发的内部上线部署系统，使用我们公司域的账号信息分配权限登录即可，可以与gitlab的仓库挂钩，提交到git上之后，在火星一号系统中，傻瓜式点击上线。
&nbsp;&nbsp;&nbsp;&nbsp;火星一号也支持代码版本的回滚。
&nbsp;&nbsp;&nbsp;&nbsp;gitlab仓库与公司内代码环境，有规定的对应关系：
* `master` 分支——对应生产环境，生产环境上线，火星一号的权限要严格
* `dev` 分支——对应T1环境，T1环境是研发团队的开发环境，部署较频繁
* `release`分支——对应T2环境，T2环境是预上线环境，即提供给测试团队使用的稳定版本

&nbsp;&nbsp;&nbsp;&nbsp;这样的话，就做到了前后端分离，后端只管自己的接口，前端负责静态界面与动态JS，谁也不影响谁。

### 4、前端部署准备
&nbsp;&nbsp;&nbsp;&nbsp;由于使用了`history`方式，界面不能有相对地址的JS、css，本来我们也是需要将这些静态文件上CDN的。
&nbsp;&nbsp;&nbsp;&nbsp;部署准备：
* 1、处理css内图片、`*.vue`文件中图片为cdn图片地址
* 2、运行`npm run build`，打包项目
* 3、js、css上cdn（生产环境）或ftp（测试环境），修改`manifest.js`相对地址
* 4、修改打包之后的index.html文件中的js、css地址
	* 如果是上线测试环境的话，js可以为ftp固定地址，可以通过设置webpack配置文件中的`publicPath`，来直接修改`index.html`中的链接地址
	* 如果是上线生产环境，cdn地址每次都会改变，这样的话，需要每次手动修改`index.html`文件

### 5、正式部署
&nbsp;&nbsp;&nbsp;&nbsp;确定好`index.html`文件处理好，提交到git，火星一号上操作即可，操作完毕，清理缓存查看结果。
&nbsp;&nbsp;&nbsp;&nbsp;如果发送错误的话，要么是前端没有写对配置参数，要么就是后端的nginx拦截没做好。


