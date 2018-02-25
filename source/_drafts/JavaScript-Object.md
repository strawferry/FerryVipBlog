---
title: JavaScript-Object
date: 2016-12-13 23:24:18
tags:
---

# 对象的操作
## 1. 对象的定义
对象是一种无序的集合数据类型，它由若干键值对组成。<br/>
JavaScript的对象用于描述现实世界中的某个对象。例如，为了描述“小明”这个淘气的小朋友，我们可以用若干键值对来描述他

``` javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};

xiaoming.name; // '小明'
xiaoming.birth; // 1990

var xiaohong = {
    name: '小红',
    'middle-school': 'No.1 Middle School' // 如果属性名包含特殊字符，就必须用''括起来
};

xiaohong['middle-school']; // 'No.1 Middle School'
xiaohong['name']; // '小红'
xiaohong.name; // '小红'
xiaohong.age; // undefined
访问不存在的属性不报错，而是返回undefined

'name' in xiaohong; // true
'grade' in xiaohong; // false
// 不过要小心，如果in判断一个属性存在，这个属性不一定是xiaoming的，它可能是xiaoming继承得到的

要判断一个属性是否是xiaoming自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法：
var xiaoming = {
    name: '小明'
};
// 因为toString定义在object对象中，而所有对象最终都会在原型链上指向object，所以xiaoming也拥有toString属性
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```