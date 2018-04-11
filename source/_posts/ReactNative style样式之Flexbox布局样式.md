---
title: ReactNative style样式之Flexbox布局样式
date: 2016-06-15 15:32:51
tags:
---
# ReactNative style样式之Flexbox布局样式
---
### Flexbox布局样式 ReactNative是参考文档大于0.29的版本
---
[参考链接2](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

[参考链接1](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

### 1. 6个属性设置在容器上
#### 1.1 任何一个容器都可以指定为Flex布局。**ReactNative无**
> **display: flex;**

> **display: inline-flex; //行内元素也可以使用Flex布局。**
![flex布局元素](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jap7mwnj21gc0va0zo.jpg)

#### 1.2 `flex-direction` 属性决定主轴的方向（即项目的排列方向）。
> `flex-direction: row(默认值) | row-reverse | column | column-reverse`;

---
> ReactNative 中的 `flexDirection`: `column`(默认值) | `column-reverse` | `row` | `row-reverse`;
![flex-direction 排列方向](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jbmm98sj21c20dy3zr.jpg)

#### 1.3 `flex-wrap` 换行
> `flex-wrap: nowrap | wrap | wrap-reverse`;

---
> ReactNative 中的 `flexWrap`: `nowrap` | `wrap` ;
![flex-wrap 换行](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jc2qtr0j215m1460zt.jpg)

#### 1.4 `flex-flow` flex-direction 和flex-wrap 的简写 **ReactNative无**
> `flex-flow : row || nowrap`;
![flex-flow](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jcg1tljj21gu0c2762.jpg)

#### 1.5 justify-content 水平排列方式
> `justify-content: flex-start | flex-end | center | space-between | space-around`;
![justify-content 水平排列方式](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jcr73b1j218m0acgnf.jpg)

---
> ReactNative中的 `justifyContent: flex-start | flex-end | center | space-between | space-around`;
![justify-content 水平排列方式](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jd9q5gbj20hp0l70sn.jpg)


#### 1.6 align-items 垂直排列方式
> `align-items: flex-start | flex-end | center | baseline | stretch`;
![align-items 垂直排列方式](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jehu5qqj21bw0a00uq.jpg)

---
>ReactNative中的 `alignItems: flex-start | flex-end | center | stretch`;
![align-items 垂直排列方式](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jewomp8j20h50lu3yg.jpg)

### 2. 容器中项目的属性
#### 2.1 order **ReactNative无**
> `order :<number>`; /* default 0 */属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
![order](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jf66cjzj20kv0dca9v.jpg)

#### 2.2 flex-grow **ReactNative无**
> `flex-grow:<number>`; /* default 0 */属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
![flex-grow](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jfhit38j20ma05v3yf.jpg)

#### 2.3 flex-shrink **ReactNative无**
> flex-shrink: <number>; /* default 1 */属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。flex-basis
![flex-shrink](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jg0qxmyj21gq0gcq6d.jpg)

#### 2.4 flex-basis **ReactNative无**
> ![flex-basis](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jgd926fj21gq0fen0l.jpg)

#### 2.5 flex **ReactNative无**
> ![flex](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jgrpxkkj21gi0i2tca.jpg)

#### 2.6 align-self
> `align-self: auto | flex-start | flex-end | center | baseline | stretch`;

---
> ReactNative中的 `alignSelf: auto | flex-start | flex-end | center | stretch`;
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1fq8jh5hubvj21ho13qdlf.jpg)

### 3. FlexBox布局目前支持React Native 的属性
```
FlexBox布局目前支持React Native 的属性有如下6个：
(1) flex :number  大于0的时候才可伸缩，按照大小显示伸缩比例；
(2) flexDirection :column(容器设置的属性:主轴方向默认－垂直方向，从上倒下)| `column-reverse` | row（水平方向，从左到右）| `row-reverse`；
(3) flexWrap :wrap(换行) －－nowrap(不换行)//容器设置的属性
(4) alignItems :flex-start | flex-end | center | stretch (容器设置的属性:伸缩项目在伸缩容器中的交叉轴的对齐方式)；
(5) justifyContent : flex-start | flex-end | center | space-between | space-aronud （容器设置的属性:伸缩项目沿着垂直方向的对齐方式）；
(6) alignSelf : flex-start | flex-end | center | auto | stretch。（伸缩项目在交叉轴的对齐方式）；
(7) position : 'absolute' | 'relative' ;
(8) zIndex : number ;
```
 