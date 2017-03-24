---
title: IE的JS兼容性问题
date: 2015-12-06 15:02:34
categories: 兼容性
tags: [兼容性,IE]
---

&nbsp;&nbsp;&nbsp;&nbsp;在与产品撕扯之后，确定了我们的系统，只支持IE9+，而且控制台系统，只支持IE11。
&nbsp;&nbsp;&nbsp;&nbsp;但就算这样，IE照样爆出bug来。

### 1、ajax强制304
&nbsp;&nbsp;&nbsp;&nbsp;例子：请求了一个列表——添加一条数据——再请求这个列表——数目不添加
&nbsp;&nbsp;&nbsp;&nbsp;打开IE的开发工具查看，数据又正常了，使用抓包工具查看，原来IE会把之前请求过的ajax地址，都当做304给处理，直接拿的缓存，没走实际的后台接口。
&nbsp;&nbsp;&nbsp;&nbsp;解决方案：ajax请求加时间戳、或加随机数、或`jquery ajax` 的`cache`设置为false
<!--more-->

### 2、汉字乱码
&nbsp;&nbsp;&nbsp;&nbsp;例子：搜索接口，输入汉字后检索，检索不出结果
&nbsp;&nbsp;&nbsp;&nbsp;抓包查看，汉字乱掉了
&nbsp;&nbsp;&nbsp;&nbsp;解决方案：ajax将检索的关键字编码，使用`encodeURIComponent`都行

### 3、表格出不来
``` html
    <table class="table-style-01">
    	<colgroup><!--如果不写colgroup的话，会挂掉-->
	        <col width="25%" />
	        ……
	    </colgroup>
        <thead>
            <tr>
                <th>分类</th>
                ……
            </tr>
        </thead>
       <tbody>
            <tr>
            ……
```
&nbsp;&nbsp;&nbsp;&nbsp;如上代码，如果不写`colgroup`的话，先进的浏览器，会把col标签，默认使用`colgroup`包起来，界面还会正常显示。
&nbsp;&nbsp;&nbsp;&nbsp;但是IE，会自作主张的用`colgroup`标签，将下面的直到tbody标签里面的内容都包起来，然后显示不了表格
&nbsp;&nbsp;&nbsp;&nbsp;解决方案：写html要符合w3c标准，不能随意简写。

### 4、`icheck`点击两次才好使的bug
&nbsp;&nbsp;&nbsp;&nbsp;`icheck`是jquery的一个优化单选、多选框的插件，在IE下，选中需要点击两下
&nbsp;&nbsp;&nbsp;&nbsp;直接使用别的css方案，替换掉`icheck`，完全是让人上火的鸡肋插件

### 5、在默认设置下，`cookie`失效
&nbsp;&nbsp;&nbsp;&nbsp;某天QA报了一个bug，IE登录不了，其余的浏览器OK，后台看了日志，说没有`cookie`。
&nbsp;&nbsp;&nbsp;&nbsp;检查了前后端代码，都没问题，忽然想起，是不是被IE禁用了`cookie`了。
&nbsp;&nbsp;&nbsp;&nbsp;IE的默认安全设置，是中级，即只信任本网站的`cookie`，不信任本网站调用第三方域名种的`cookie`，刚好我们的就是不同的域名。
&nbsp;&nbsp;&nbsp;&nbsp;把权限放到最低，就好使了。
&nbsp;&nbsp;&nbsp;&nbsp;解决方案：
* 1、`cookie`本域名种植
* 2、IE下，给出单独提示，提示把权限打开

### 总结：
&nbsp;&nbsp;&nbsp;&nbsp;其余的像`event`事件、dom操作、宽高获取兼容性问题，已经被大家知悉，jquery已经帮大家处理掉这些兼容性问题，但是还会经常有一些注意不到的细节。
&nbsp;&nbsp;&nbsp;&nbsp;`IE该死`
&nbsp;&nbsp;&nbsp;&nbsp;`IE6-8更该死`

