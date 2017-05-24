---
title: 跨域:（四）chrome浏览器本地跨域——Mac
date: 2015-09-07 15:02:34
categories: 跨域
tags: [跨域, chrome]
---

类似于Windows下的chrome，也需要先创建个个人目录，如`/Users/zhaoshengdi/MyChromeDevUserData/`
然后将已打开的chrome退出，运行如下命令：
``` shell 
open -a'Google Chrome' --args --disable-web-security --user-data-dir=/Users/zhaoshengdi/MyChromeDevUserData/ --allow-running-insecure-content
```

这样的话，也会启动一个无需进行任何设置，就可以跨域操作的浏览器，进行接口的调试等相关工作。