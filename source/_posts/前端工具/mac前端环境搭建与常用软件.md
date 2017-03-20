---
title: Mac前端环境搭建与常用软件
date: 2017-03-19 15:02:34
categories: 前端工具
tags: [Mac]
---

&nbsp;&nbsp;&nbsp;&nbsp;最近，在我的大力鼓吹下，我们组的同学们，都陆续申请到了mac电脑，鸟枪换炮了，然后给他们好几个人都挨个讲了一遍Mac的使用、常用软件等等，费劲口舌，现在总结一下，再来新人的话，直接拿文档去怼他。(也可以参考[前端工具集合-本站](http://localhost:4000/2017/03/23/%E5%89%8D%E7%AB%AF%E5%B7%A5%E5%85%B7/%E5%89%8D%E7%AB%AF%E5%B7%A5%E5%85%B7%E9%9B%86%E5%90%88/))

### 1、旧电脑备份
&nbsp;&nbsp;&nbsp;&nbsp;在拿到Mac电脑之后，Windows电脑需要还回去，所以需要做好备份
#### 1、1 代码备份
* 公司项目代码，git、svn上备份
* 个人代码，github备份
<!--more-->

#### 1、2 文件备份
* 都可以存百度云盘
* 脑图文件，可以存百度脑图

#### 1、3 笔记备份
* 有道云笔记
* 印象笔记
* 其余在线博客

#### 1、4 浏览器收藏夹备份
* 登录chrome的个人账户，同步收藏夹（需要翻墙）
* 通过其余浏览器的个人账户备份云端收藏夹

#### 1、5 其余需要备份的内容
* 个人重要聊天信息
* 个人相关密码
* 个人图片

#### 1、6 最后，确保全部备份之后，删除掉旧电脑的个人隐私信息
&nbsp;&nbsp;&nbsp;&nbsp;接下来，可以把玩Mac了

### 2、熟悉Mac

* Mac系统十分复杂，首先熟悉一下Mac F1——F12的快捷键
* 熟悉一下触摸板操作，根据个人情况，是否配置轻触点击、三指拖动
* 习惯使用`command`键替换`control`键
* 找到终端的所在位置
* 习惯finder替换我的电脑
* 根据个人习惯，删除、添加、排序下面Dock上的菜单
* 学习Mac常见命令（这个可以以后再说）
* 登录上`APP Store`，开始下载程序

### 3、下载安装常用程序
* 首先下载chrome，需要通过Safari下载。然后安装chrome扩展工具([前端常用chrome扩展程序-本站](http://localhost:4000/2017/03/22/%E5%89%8D%E7%AB%AF%E5%B7%A5%E5%85%B7/%E5%89%8D%E7%AB%AF%E5%B8%B8%E7%94%A8chrome%E6%89%A9%E5%B1%95%E7%A8%8B%E5%BA%8F/))
* 通过APP Store或者chrome，下载相关程序
* 输入法——推荐搜狗
* QQ、微信
* 在邮件里面配置邮箱账户信息
* 下载安装Firefox
* 下载安装百度云盘
* 下载安装安装office套件，这个需要破解
* 下载安装音乐、视频、迅雷等个人使用程序

### 4、鼓捣前端环境
* Mac安装xcode之后，会自带Mac，安装xcode吧，以后早晚用得到
* git安装完成之后，配置相关ssh key，省得以后来回输入账户、密码
* 安装nodejs，安装gulp、hexo等必要的npm全局包（[前端常用npm全局包-本站](http://localhost:4000/2017/03/20/%E5%89%8D%E7%AB%AF%E5%B7%A5%E5%85%B7/%E5%89%8D%E7%AB%AF%E5%B8%B8%E7%94%A8npm%E5%85%A8%E5%B1%80%E5%8C%85/)）
* 全局安装时，你会发现没有权限，简单的解决方式是使用`sudo npm install xxx -g`，然后输入密码即可，还有一种方法，就是安装`homebrew`，获取全局权限，还可以通过`homebrew`安装其余的软件，如nodejs、mongodb等。
* 安装代码编辑工具（或叫前端IDE），推荐sublime（[sublime插件推荐-本站](http://localhost:4000/2017/03/19/前端工具/sublime插件推荐/)）
* 安装抓包、代理工具，推荐使用`Charles`,使用类似于Windows环境下的fiddler，fiddler由于是使用.NET编写，无法使用到Mac环境中。
	* 开始`Charles`，会提示Java环境错误，百度一下，下载安装一个jar包就可以解决
* 绑定host工具，推荐使用Gas Mask
* ftp工具，使用FileZilla
* 翻墙工具，自己购买的vpn，或者自己下载的绿色翻墙工具，这个大家都懂的
* 上面是必需安装的，如果需要开发后台程序的话，下面的还需要按需安装
	* `MySQL`
	* `navicat for mysql`，可视化查看MySQL工具
	* `mongodb`
	* `robomongo`，可视化查看mongodb工具
* 微信小程序开发工具，假如你现在还看还小程序的话
* 到此为止，你可以拉代码，愉快的coding了，不过还可以继续

### 5、前端周边工具
* Photoshop
* 百度脑图网页版、xmind——思维工具
* `axure`——产品原型查看
* `teamview`——远程控制工具
* 云端笔记，有道云笔记、印象笔记等等
……差不多就这样了，工具已经差不多了，赶紧去撸代码吧。

### 6、附加个人电脑桌面
<!-- <img src="http://localhost:4000/images/fanyi3.png" alt="node控制台" style="width:70%"> -->
![第一屏](http://localhost:4000/images/mac1.png)
![第二屏与Dock](http://localhost:4000/images/mac2.png)






