---
title: JavaScript-Array
date: 2016-12-13 21:58:44
tags: ["JavaScript", "Array", "数组操作"]
---

# 数组的学习和操作
## 1. 数组的定义
JavaScript的Array可以包含任意数据类型，并通过索引来访问每个元素。


``` javascript
var arr = [1, 2, 3];
arr.length; // 3 获取长度
arr.length = 6;
arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
arr.length = 2;
arr; // arr变为[1, 2]
arr.length = 0; // 清空数组

arr[1] = 99; // 通过索引把对应的元素修改为新的值
// 索引超过了范围，同样会引起Array大小的变化
arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
```

## 2. 操作数组
### 2.1 `indexOf` 搜索一个指定的元素的位置
``` javascript
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(10); // 元素10的索引为0
arr.indexOf(20); // 元素20的索引为1
arr.indexOf(30); // 元素30没有找到，返回-1
arr.indexOf('30'); // 元素'30'的索引为2
```
### 2.2 `slice` 切片,对应String的substring()版本,截取
``` javascript
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```
### 2.3 `push` 向Array的末尾添加若干元素，`pop` 则把Array的最后一个元素删除掉
``` javascript
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```
### 2.4 `unshift` 头部添加若干元素, `shift` 则把Array的第一个元素删掉
``` javascript
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
```
### 2.5 `sort` 对当前Array进行排序，它会直接修改当前Array的元素位置，直接调用时，按照默认顺序排序
``` javascript
var arr = ['B', 'C', 'A'];
arr.sort();
arr; // ['A', 'B', 'C']
```
### 2.6 `reverse` 反转整个Array的元素
``` javascript
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
```
### 2.7 `splice` 可删除从 index 处开始的零个或多个元素，并且用参数列表中声明的一个或多个值来替换那些被删除的元素。
splice(index,howmany,item1,.....,itemX)
splice() 方法与 slice() 方法的作用是不同的，splice() 方法会直接对数组进行修改。

|  参数 |  描述 |
|:-:|---|
|  index |  必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 |
|  howmany |  必需。要删除的项目数量。如果设置为 0，则不会删除项目。 |
|  item1, ..., itemX | 可选。向数组添加的新项目。  |
>返回值 

| 类型 |  描述  |
|:-:|---|
|  Array |  包含被删除项目的新数组，如果有的话。|

	
	
``` javascript
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```
### 2.8 `concat` 把当前的Array和另一个Array连接起来，并返回一个新的Array
``` javascript
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']
```
### 2.9 `join` 把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串
``` javascript
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3' 如果Array的元素不是字符串，将自动转换为字符串后再连接
```
### 2.10 多维数组
``` javascript
var arr = [[1, 2, 3], [400, 500, 600], '-'];
```
### 2.11 `map` 和 `reduce`
``` javascript
var pow = function (item,index,list) {
    return item * item;
};
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
arr.map(pow); // [1, 4, 9, 16, 25, 36, 49, 64, 81]
// map()作为高阶函数，事实上它把运算规则抽象了
arr.map(String); // ['1', '2', '3', '4', '5', '6', '7', '8', '9']
// 把Array的所有数字转为字符串

 array1.reduce(callbackfn, initialValue)
// array1: 必需。一个数组对象。
// initialValue: 可选。如果指定 initialValue，则它将用作初始值来启动累积。第一次调用 callbackfn 函数会将此值作为参数而非数组值提供。
// callbackfn: 必需。一个接受最多四个参数的函数。对于数组中的每个元素，reduce 方法都会调用 callbackfn 函数一次。

function callbackfn(previousValue, currentValue, currentIndex, array1)

// previousValue: 通过上一次调用回调函数获得的值。如果向 reduce 方法提供 initialValue，则在首次调用函数时，previousValue 为 initialValue。
// currentValue: 当前数组元素的值。
// currentIndex: 当前数组元素的数字索引。
// array1: 包含该元素的数组对象。
```
### 2.12 `filter` 过滤,它用于把Array的某些元素过滤掉，然后返回剩下的元素,根据返回值是true还是false决定保留还是丢弃该元素
``` javascript
var arr = ['A', 'B', 'C'];
var r = arr.filter(function (element, index, self) {
    console.log(element); // 依次打印'A', 'B', 'C'
    console.log(index); // 依次打印0, 1, 2
    console.log(self); // self就是变量arr
    return true;
});
```
### 2.13 `sort` 排序
``` javascript
// 看上去正常的结果:
['Google', 'Apple', 'Microsoft'].sort(); // ['Apple', 'Google', 'Microsoft'];
// apple排在了最后:
['Google', 'apple', 'Microsoft'].sort(); // ['Google', 'Microsoft", 'apple']
// 无法理解的结果:
[10, 20, 1, 2].sort(); // [1, 10, 2, 20]
// 第二个排序把apple排在了最后，是因为字符串根据ASCII码进行排序，而小写字母a的ASCII码在大写字母之后。
// 第三个排序结果是什么鬼？简单的数字排序都能错？这是因为Array的sort()方法默认把所有元素先转换为String再排序，结果'10'排在了'2'的前面，因为字符'1'比字符'2'的ASCII码小

// sort()方法也是一个高阶函数，它还可以接收一个比较函数来实现自定义的排序
var arr = [10, 20, 1, 2];
arr.sort(function (x, y) {
    if (x < y) {
        return -1;
    }
    if (x > y) {
        return 1;
    }
    return 0;
}); // [1, 2, 10, 20]
// sort()方法会直接对Array进行修改，它返回的结果仍是当前Array
```














