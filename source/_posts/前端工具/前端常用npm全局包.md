---
title: 前端常用npm全局包
date: 2017-03-20 13:06:34
categories: 前端工具
tags: [前端工具,npm]
---

&nbsp;&nbsp;&nbsp;&nbsp;就现在做前端工作而言，不会node、不会鼓捣npm的话，已经严重落伍了，落伍到不行了。
&nbsp;&nbsp;&nbsp;&nbsp;npm有一些非常有用的全局包，在生成项目框架、运行本地开发环境时，会大大提高我们的生成力。
&nbsp;&nbsp;&nbsp;&nbsp;首先，在终端输入`npm list -g --depth 0`命令，查看本机已经安装的全局包。
<!--more-->

``` shell
├── create-react-app@1.1.0
├── docsify-cli@3.0.1
├── electron@1.4.15
├── electron-packager@8.5.1
├── express@3.5.0
├── express-generator@4.13.4
├── gitbook-cli@2.3.0
├── gulp@3.9.1
├── hexo-cli@1.0.2
├── http-server@0.9.0
├── jekyll@3.0.0-beta1
├── jshint@2.9.2
├── n@2.1.4
├── npm@3.10.10
├── nuxt@0.9.9
├── nvm@0.0.4
├── react-native-cli@1.0.0
├── vue-cli@2.8.1
├── webpack@1.13.2
└── weex-toolkit@0.6.4
```
&nbsp;&nbsp;&nbsp;&nbsp;如上所示，是我电脑本机安装的npm包，接下来我会分类介绍一下。

### 1、前端项目脚手架、基础支撑类

``` shell
├── create-react-app // 是创建react单界面应用的脚手架
├── electron、electron-packager // 开发桌面程序的脚手架与支撑
├── nuxt // 基于vue技术开发后端渲染界面的技术
├── react-native-cli // 开始react native的脚手架
├── vue-cli // 创建vue webapp的脚手架
├── weex-toolkit // 开发weex的组件
```

&nbsp;&nbsp;&nbsp;&nbsp;由此可见，现在只要是流行的大技术框架，都会提供脚手架来加速开发者的使用。
&nbsp;&nbsp;&nbsp;&nbsp;前几天我也试玩过angular2，angular2也提供了脚手架，不过我没安装全局的包。
&nbsp;&nbsp;&nbsp;&nbsp;超链接：
* [create-react-app](https://github.com/facebookincubator/create-react-app)
* [electron](https://electron.atom.io/)
* [nuxt](https://cn.nuxtjs.org/)
* [react-native-cli](https://www.npmjs.com/package/react-native-cli/)
* [vue-cli](https://github.com/vuejs/vue-cli)
* [weex-toolkit](https://weex.apache.org/cn/)

### 2、在线博客、文档项目脚手架类

``` shell
├── docsify-cli // 是一个类似与hexo的在线博客生成器，支持markdown语法，样式、交互效果与vuejs官网样式类似，比较小众
├── gitbook-cli // gitbook的脚手架，也是支持markdown语法，这个很流行，写在线api、在线教程什么的比较适合
├── hexo-cli // 在线博客生成器，也是支持markdown语法，直接生成静态界面，可以与github链接，一键推送
├── jekyll // 在线博客生成器，与hexo类似，配置复杂一些
```

&nbsp;&nbsp;&nbsp;&nbsp;由于我最近喜欢写博客，研究过好几种在线博客技术，最终选择了gitbook与hexo，前者写教程、api之类的，后者写普通博客一类的。
&nbsp;&nbsp;&nbsp;&nbsp;也得出一个趋势，前端博客，现在都建议使用markdown语法，不会markdown的话，也是一种落伍。
&nbsp;&nbsp;&nbsp;&nbsp;超链接：
* [docsify](https://docsify.js.org/#/)
* [gitbook-cli](https://www.npmjs.com/package/gitbook-cli)
* [hexo](https://hexo.io/)
* [jekyll](http://jekyll.com.cn/)

### 3、npm相关
``` shell
├── n // npm的版本管理工具，用于切换node版本
├── npm // npm 自己的包
├── nvm // npm的另一个版本管理工具，类似于n
```
### 4、服务器相关
``` shell
├── express 、 express-generator // express开发nodejs后台程序
├── http-server // 启动静态http服务器，可以在任意目录下启动
```
&nbsp;&nbsp;&nbsp;&nbsp;超链接：
* [http-server](https://www.npmjs.com/package/http-server)

### 5、前端自动化类
``` shell
├── gulp // 前端自动化工具，老牌的
├── webpack // 前端工程化工具，大有统一前端工具之势
```
### 6、其余
``` shell
├── jshint // 一种JS代码风格检测工具，是在sublime中高亮显示，需要nodejs配合
```

### 7、总结
&nbsp;&nbsp;&nbsp;&nbsp;上面的全局包列表，有些不一定必须要全局安装，但是由于使用频率太高，就全局安装了省事了。
&nbsp;&nbsp;&nbsp;&nbsp;全局包已经有这么多，各自项目中依赖的包，就更多了，npm管理JS包，是大势所趋。

