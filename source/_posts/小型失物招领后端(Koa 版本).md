
---
title: 小型失物招领后端(Koa 版本)
date: 2018-02-24 13:23:42
tags:
---

# 小型失物招领后端(Koa 版本)

## 项目说明
本身是搞 iOS 的后面入了 ReactNative 的坑,慢慢的就比较多的接触 JavaScript ,还有就是 JavaScript 慢慢的可以做的东西越来越多;
不仅可以做前端网页,还可以做移动端 App(ReactNative),还能做后端(Node.js),还有其他的;

这个失物招领是为了练手 Node.js,同时也为了配合这个写了个 App 前端(iOS 和 安卓),链接在后面也会放出了;

目前主要的 Feature:  
1. 用户登录注册;
2. 基本的管理员权限管理;
3. 失物招领信息发布,关注收藏,通知审核等;
4. 管理员的基本功能的管理与审核;
5. 极光推送对接,使内容实时推送给用户;

## 本地运行条件

* MongoDB 数据库
* Node.js 环境

## 基础配置

1. 七牛配置
   1. 七牛配置是为了保存图片到七牛;
   2. 申请相应的开发者账号,填入到 `config文件夹的config文件`;
   3. 配置错误,或未配置调用到会导致程序崩溃;

> ![](http://ww1.sinaimg.cn/large/8bbf0afbly1form5qgmtaj21x20yin26.jpg)
> ![](http://ww1.sinaimg.cn/large/8bbf0afbly1form5qgpx8j21x013qn4q.jpg)

2. 极光配置
   1. 使消息即使让用户知道;
   2. 申请相应的开发者账号,填入到 `config文件夹的config文件`;
   3. 配置错误,或未配置调用到会导致程序崩溃;

> ![](http://ww1.sinaimg.cn/large/8bbf0afbly1form5qgf31j21ui196jxm.jpg)

## 造一些假数据的

项目目录下执行 `node data.js` 两次就行;

```
    超级管理员
    用户名: admin@163.com
    密码: 123456
    其他的用户: user[1 - 10]@163.com 密码: 123456
```
  

## 启动

* 本地启动 
  1. 首先启动本地 MongoDB 数据库,项目目录下执行 `npm run mongo` 数据库跑默认的段口;
  2. 项目目录下执行 `npm start` 启动;
  3. [就可以打开文档 http://localhost:5566/docs/](http://localhost:5566/docs)
  
* 服务器部署(主要使用 `pm2` 部署)
  1. 服务器安装 `node` `pm2` `MongoDB` 环境等; 
  2. 项目目录下执行 
     1. 测试 `pm2 start dev.json`
     2. 正式 `pm2 start dev.json`
  3. 查看日志 `pm2 logs`

## 对应的客户端

* 目前就只做了 App 端,按理说目前接口基本可以做个网页前端的,微信公众号以及小程序,在做些修改也是应该可以的;

## 下载体验
iOS 没有发布,下载安卓体验

[安卓 fir.im 下载](https://fir.im/cpt1)

或者直接扫码下载
> ![扫码下载](data:image/png;base64,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)



## 仓库地址

[Express 版本 GitHub 地址,具体配置看文档](https://github.com/strawferry/lostserver)

[Koa 版本 GitHub 地址,具体配置看文档](https://github.com/strawferry/openlostkoa)

[App 地址,具体配置看文档](https://github.com/strawferry/lostapp)

# 个人博客
### **博客地址: [`https://cblog.ferryvip.com/`](https://cblog.ferryvip.com/)**