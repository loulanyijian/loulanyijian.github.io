---
title: es6在实际工作中的使用
date: 2017-05-24 15:02:34
categories: es6
tags: [es6]
---

`你用了es6没？没有？那你还是前端么？`
`/(ㄒoㄒ)/~~`
`那赶紧跟着老司机上车吧`

### let & const

变量使用let，常量使用const，解决了变量提升，又从代码层面对数据引用错误做了限制。总之，决不能出现var

### 解构赋值

要用数组、对象的解构赋值，千万别挨个赋值，不高大上啊

### 基础、复杂类型的扩展

* 字符串模板
	
	字符串拼接千万不用+，要使用`${obj.xx}`，还可以支持回车

* 函数默认参数

	不用写 || 这种短路写法了，直接在传参的时候搞定

* rest参数

	不用写arguments了

* 箭头函数
	
	不用写function了，虽然难读，但是可以合并到一行啊。但是在vue中使用的话，要注意this的指向啊

* 数组

	* Array.from ——转变成数组更简单啦
	* entries()，keys() 和 values() ——遍历起来更简单啦

* 对象

	* 属性可以简洁表达了
	* Object.keys()，Object.values()，Object.entries() ——遍历更简单了
	* ...扩展运算符，赋值、转化，无所不能

### set & map

终于不用使用自己模拟数据结构了

### Promise

可以摆脱回调地狱了，虽然平常也嵌套几层回调

### Iterator 和 for...of

又多了一种遍历的方式了

### Generator & yield

es6的异步编程呐，虽然马上就要被es7的asnyc & await取代了

### asnyc & await

es7的异步编程，真正的未来，已经到来。koa2也是用的他，nodejs已经支持

### Class继承

终于可以像写Java一样写继承了，不用写冗长的Prototype了

### import & export

未来的模块化，什么AMD、CMD、commonjs，都是浮云，import，才是王道，虽然还不支持自动化引入，但是总算不用写额外的配置文件来处理依赖了

### 总结

能用ES6的，不用ES5，能用ES7的，不用ES6，越新越好，反正有babel撑腰




