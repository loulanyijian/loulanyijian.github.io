---
title: js sort方法根据数组中对象的某一个属性值进行排序
date: 2017-04-23 10:02:34
categories: 技术大杂烩
---

get到一个实用技能，sort方法接收一个函数作为参数，这里嵌套一层函数用来接收对象属性名，其他部分代码与正常使用sort方法相同

``` javascript
var arr = [
    {name:'zopp',age:0},
    {name:'gpp',age:18},
    {name:'yjj',age:8}
];
  
function compare(property){
    return function(a,b){
        var value1 = a[property];
        var value2 = b[property];
        return value1 - value2;
    }
}
console.log(arr.sort(compare('age')))
```
![js sort](http://img.blog.csdn.net/20160918145611606)

[原文链接](http://blog.csdn.net/qq_17335153/article/details/52574531)

