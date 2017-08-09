---
title: JavaScript-String
date: 2016-12-13 21:34:28
tags: ["JavaScript", "String", "字符串操作"]
---
#  字符串学习操作

## 1. 字符串定义
'字符串' 和 "字符串" 字符串用单引号和双引号表示, 不过要同样的成对出现;<br>
如果 `'` 本身也是一个字符，那就可以用 `""` 括起来 `"I'm OK"` <br>
如果字符串内部既包含 `'` 又包含 `"` 怎么办？可以用转义字符\来标识;

``` javascript
'I\'m \"OK\"!';
```

## 2. 模板字符串, 多行字符串(ES6 标准)
ES6新增了一种模板字符串，表示方法和上面的多行字符串一样，但是它会自动替换字符串中的变量：

``` javascript
var str = `这是一个
多行
字符串`;
var name = '小明';
var age = 20;
alert(`你好, ${name}, 你今年${age}岁了!`);
```

## 3. 操作字符串

``` javascript
var s = 'Hello, world!';
s.length; // 13
//要获取字符串某个指定位置的字符，使用类似Array的下标操作，索引号从0开始;
s[0]; // 'H'
s[7]; // 'w'
s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined
// 字符串不可改变
```

### 3.1 `toUpperCase` 字符串全部变大写`toLowerCase` 字符串全部变小写
``` javascript
var s = 'Hello';
s.toUpperCase(); // 返回'HELLO'
s.toLowerCase(); // 返回'hello'
```
### 3.2 `indexOf`会搜索指定字符串出现的位置：
``` javascript
var s = 'hello, world';
s.indexOf('world'); // 返回7
s.indexOf('World'); // 没有找到指定的子串，返回-1
```
### 3.3 `substring` 返回指定索引区间的子串
``` javascript
var s = 'hello, world'
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
s.substring(7); // 从索引7开始到结束，返回'world'
```










