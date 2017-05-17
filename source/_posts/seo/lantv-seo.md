---
title: 蓝TV SEO优化
date: 2015-07-29 15:02:34
categories: SEO
tags: [SEO]
---

最近开发了浙江广电的蓝TV项目，成功上线运行，网址[http://tv.cztv.com/](http://tv.cztv.com/)。
合作的统计提供端——国双科技，提供一份需要SEO优化的文档，主要包括如下内容：

### 1、网站地图分类列表页Title及URL优化
* 将`<title>综艺 -  - 中国蓝TV</title>`修改为`<title>综艺-网站地图-中国蓝TV</title>`
* `http://list.cztv.com/sitemap/c11_s_t_a_y_f_st_vt_ph_lg_tv_sp_md_o9_d_p.html` 这种URL过长，需要优化

### 2、专题页面URL优化（避免直接使用搜索URL作为页面URL）

* 将`http://so.cztv.com/pc/s?wd=中国梦想秀`替换为`http://tv.cztv.com/zongyi/zzmxx`

### 3、播放页相关剧集内容可见性优化
<!-- more -->

* 播放页中的相关剧集链接对搜索引擎不可见，搜索引擎无法抓取相关剧集中的内容。从整站的角度来看，所有的相关剧集都不可见，严重影响搜索引擎对页面中内容的正常抓取。（爱奇艺、优酷等视网站相关剧集源代码可见的，因此，可参考对应修改）

![seo](http://localhost:4000//images/seo.png)

### 4、CMS中sitemap生成功能开发实施


* 最简单的 Sitemap 形式，就是XML 文件，在cms端，自动更新Sitemap。

### 后记
在开发完成静态HTML界面时，国双科技也提供了一份优化方案，检查了各个界面的标签结构，从seo的角度，提出了修改意见。大体就是`H1-H6`标签、P标签什么的。