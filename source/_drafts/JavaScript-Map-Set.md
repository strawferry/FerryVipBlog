---
title: JavaScript-Map-Set
date: 2016-12-13 23:41:10
tags: ["JavaScript", "Map", "Set"]
---
# 1. `Map(ES6)` 是一组键值对的结构，具有极快的查找速度。

``` javascript
var m1 = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m1.get('Michael'); // 95

var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined

// 由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉
var m = new Map();
m.set('Adam', 67);
m.set('Adam', 88);
m.get('Adam'); // 88
```
# 2. `Set(ES6)` 一组key的集合，但不存储value。由于key不能重复，所以，在Set中，没有重复的key

``` javascript
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3

// 重复元素在Set中自动被过滤
var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}

// add(key) 方法可以添加元素到Set中, 可以重复添加，但不会有效果
s.add(4)
s // {1, 2, 3, 4}
s.add(4)
s // {1, 2, 3, 4}
// delete(key)方法可以删除元素
s.delete(3);
s; // Set {1, 2}
```
# 3. `iterable` ES6标准引入了新的iterable类型, Array、Map和Set都属于iterable类型。具有iterable类型的集合可以通过新的for ... of循环来遍历
``` javascript
var a = ['A', 'B', 'C'];
var s = new Set(['A', 'B', 'C']);
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
for (var x of a) { // 遍历Array
    alert(x);
}
for (var x of s) { // 遍历Set
    alert(x);
}
for (var x of m) { // 遍历Map
    alert(x[0] + '=' + x[1]);
}
```
你可能会有疑问，`for ... of` 循环和 `for ... in` 循环有何区别？
`for ... in` 循环由于历史遗留问题，它遍历的实际上是对象的属性名称。一个Array数组实际上也是一个对象，它的每个元素的索引被视为一个属性

``` javascript
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x in a) {
    alert(x); // '0', '1', '2', 'name'
}
for ... in循环将把name包括在内，但Array的length属性却不包括在内。

for ... of循环则完全修复了这些问题，它只循环集合本身的元素
for (var x of a) {
    alert(x); // 'A', 'B', 'C'
}
```
更好的方式是直接使用 `iterable` 内置的 `forEach` 方法，它接收一个函数，每次迭代就自动回调该函数

```javascript
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    alert(element);
});
// Set与Array类似，但Set没有索引，因此回调函数的前两个参数都是元素本身
var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    alert(element);
});
// Map的回调函数参数依次为value、key和map本身
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
m.forEach(function (value, key, map) {
    alert(value);
});
//如果对某些参数不感兴趣，由于JavaScript的函数调用不要求参数必须一致，因此可以忽略它们。例如，只需要获得Array的element
var a = ['A', 'B', 'C'];
a.forEach(function (element) {
    alert(element);
});
```