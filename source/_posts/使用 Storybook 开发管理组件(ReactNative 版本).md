---
title: 使用 Storybook 开发管理组件(ReactNative 版本)
date: 2019-07-25 16:26:34
tags:
---

# 使用 Storybook 开发管理组件(ReactNative 版本)

## 0. 介绍
[Storybook](https://storybook.js.org) 是 UI 组件的开发环境。它允许您浏览组件库，查看每个组件的不同状态，以及交互式开发和测试组件。

根据官网的介绍可以支持 `React,React Native,Vue,Angular,Ember,HTML,Svelte,Mithril,Riot`.

做了不少 ReactNative 的项目,每个项目的组件不少,开发到最后都不知道有多少个,如何使用,所以才会想着用啥管理起来,我这次讲的就是关于 React Native 的一些简单使用方法;

## 1. [安装(ReactNative 版本)](https://storybook.js.org/docs/guides/guide-react-native/)
* Automatic setup 自动安装,通过官方的 `@storybook/cli` 命令行创建 

	`npx -p @storybook/cli sb init --type react_native`
	
	* 是否安装 web server 选取

		> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5byy5hvrmj21no0vq7a7.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5byy5lhepj21no0vqtda.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5byy5fi6pj21jy144na8.jpg)
安装完成,一些依赖,以及文件目录

	* 启动项目

		> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5byy5yakej20q81g0wq9.jpg)
	发现会有依赖缺失,缺失的依赖安装(估计是当前版本缺失吧)
	`yarn add -D emotion-theming @emotion/core`
	![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5byy5kfm6g208e0gkgu5.gif)运行成功
	
	* `yarn storybook` 启动 web server 管理
		> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5byy5k5paj22081d018u.jpg)

* Manual setup 手动安装,自己添加依赖,以及配置文件位置(稍微麻烦点)
	
	`yarn add -D @storybook/react-native @storybook/addons @storybook/addon-links @storybook/addon-actions emotion-theming @emotion/core babel-loader @storybook/react-native-server`
	
	文件目录的就可以参照自动创建的,或者跟着[官方教程](https://storybook.js.org/docs/guides/guide-react-native/)
做,这边就不在展开,基本后面展示和上面一样

## 2. [插件 addon](https://storybook.js.org/addons/)
刚才跑起来的项目点击到 ADDONS 里面显示没有配置加载,这里就说下插件已经配置
首先是一张官方 addon 插件支持表,可以看出 React 支持的最多, rn 的支持偏少而且支持配置比较复杂,接下来继续看
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5bzxfrlx0j21dy1f4wm1.jpg)

### 2.1 [@storybook/addon-actions | @storybook/addon-ondevice-actions](https://github.com/storybookjs/storybook/tree/master/addons/actions)
Storybook Addon Actions可用于显示Storybook中事件处理程序接收的数据。

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5c1fkd964j20r01g4q4p.jpg)

### 2.2 [@storybook/addon-notes | @storybook/addon-ondevice-notes](https://github.com/storybookjs/storybook/tree/next/addons/notes)
Storybook Addon Notes允许您在Storybook中为故事编写注释（文本或HTML）。

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5c2avs030j20r01g4tah.jpg)

### 2.3 [@storybook/addon-links](https://github.com/storybookjs/storybook/tree/next/addons/links)
Storybook Links addon 可用于创建在故事书中的故事之间导航的链接。在 ReactNative 中链接跳转这个版本好像有点问题,待跟进看下

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5c2msbup2g207w0fi79q.gif)

### 2.4 [@storybook/addon-backgrounds | @storybook/addon-ondevice-backgrounds](https://github.com/storybookjs/storybook/tree/next/addons/backgrounds)
Storybook Background Addon 可用于更改故事书中预览中的背景颜色。

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5c2y0e85yg207w0fi0wd.gif)

### 2.5 [@storybook/addon-knobs | @storybook/addon-ondevice-knobs](https://github.com/storybookjs/storybook/tree/next/addons/knobs)
Storybook Addon Knobs 允许您使用Storybook UI动态编辑React道具。您还可以使用旋钮作为Storybook中故事的动态变量。

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5c35lg0pbg207w0fiada.gif)

### 2.6 [@storybook/addon-options](https://github.com/storybookjs/storybook/tree/next/addons/options)
* NOTE: Options Addon is deprecated as of Storybook 5.0,直接内嵌
	* Global options: addParameters({ options: { ... }}) and no addon is needed.
	* Story options: storiesOf(...).add('name', storyFn, { options: { ... }})

## 3.总结
* Storybook 可以通过给每个组件写 story ,然后显示一些使用案例,同时可以根据一些 addon 插件,做到直接调试 UI,同时这样也能很好的管理组件;

* 可以通过官方给的 [addon API](https://storybook.js.org/docs/addons/api/) 自己写一些好用的插件,可以参考 [官方教程](https://storybook.js.org/docs/addons/writing-addons/)


## 相关链接
* [GitHub 示例代码地址](https://github.com/strawferry/storybookrn.git)
* [Storybook GitHub](https://github.com/storybookjs/storybook)
* [Storybook 官网](https://storybook.js.org)