---
title: Jenkins 基本食用方法
date: 2019-07-22 14:50:48
tags:
---

# Jenkins 基本食用方法

## 0. 介绍
Jenkins是一个开源软件项目，是基于Java开发的一种持续集成工具，用于监控持续重复的工作，旨在提供一个开放易用的软件平台，使软件的持续集成变成可能。

Jenkins功能包括：

1. 持续的软件版本发布/测试项目。
2. 监控外部调用执行的工作。

## 1. 安装(Mac OS)
通过 brew 安装 Jenkins,其中可能还需要 Java 环境依赖,需要去[官网下载](https://www.oracle.com/technetwork/java/javase/downloads/index.html) jdk,我这边用的是 [jdk1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

安装: `brew install jenkins`

* 直接启动: `jenkins` 就可以启动,退出命令行就关闭服务

* 通过 `brew services`

	启动: `brew services start jenkins`  

	重启: `brew services restart jenkins`

	关闭: `brew services stop jenkins`
	
## 2. 初始配置
第一次安装后启动需要做初始配置

* 解锁 Jenkins ,从命令行或者提示的路径找到密码

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58i9ovvlej22rs12awsx.jpg)
* 自定义一些扩展插件,可选择安装推荐的或者自选,选择推荐安装,后续管理插件还能继续安装

>![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58i9ojhlaj21kq0ycae5.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58i9p3i4zj21ku10eqc4.jpg)

* 创建管理账户

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58j1ckpdwj21ke0zygot.jpg)

* 然后就进入 Jenkins 了

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58j1bttb2j21oy0zqn0w.jpg)

* 插件的查找和安装

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58j1c07o1j21p614e11w.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58j1bs7jjj21ro0xcwkg.jpg)

* 简单的创建任务

> 创建任务,给任务起一个名
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58k5cd6z0j21ro1e4qd3.jpg)
任务做配置,如 描述,Git,构建等;
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58k5cdp55j21e628ealp.jpg)
任务构建,以及进度条
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58k5c7y2hj226k0wmn23.jpg)
构建日志输出
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58k5cfwn7j226w140dtn.jpg)

## 3.一些好用的插件
* [动态参数构建 Dynamic Extended Choice Parameter](https://wiki.jenkins.io/display/JENKINS/Dynamic+Extended+Choice+Parameter+plugin)
* [Git 参数 Git Parameter](https://wiki.jenkins.io/display/JENKINS/Git+Parameter+Plugin)

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58ljspuc7j233r26nnj2.jpg)

* [Build Name Setter](https://wiki.jenkins.io/display/JENKINS/Build+Name+Setter+Plugin)
* [设置构建后描述 Project Description Setter](https://wiki.jenkins.io/display/JENKINS/Project+Description+Setter+Plugin)

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58ltjmgxqj231p1y2nkr.jpg)

* [设置强制语言包 Locale](https://wiki.jenkins.io/display/JENKINS/Locale+Plugin)

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58m3hjdcij23be1fe4gz.jpg)


## 4. 一些问题解决
* 有些时候 git 内容很大,pull 时会出现超时导致构建失败!

解决方式:  Git 配置时添加一个 clone 的配置把超时改为 60 或者更多,把超时改大,一般就第一次的 pull 会请求比较久,后续都是增量的,会比较快了;
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g58faae3lij227a1ew47n.jpg)

## 5. 等等
等待继续研究,估计是和 docker 相关的!