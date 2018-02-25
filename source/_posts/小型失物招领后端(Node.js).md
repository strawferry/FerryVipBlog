---
title: 小型失物招领后端(Node.js)
date: 2018-02-24 13:23:42
tags:
---

# 小型失物招领后端(Node.js)

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
  3. [就可以打开文档 http://localhost:5566/docs](http://localhost:5566/docs)
  
* 服务器部署(主要使用 `pm2` 部署)
  1. 服务器安装 `node` `pm2` `MongoDB` 环境等; 
  2. 项目目录下执行 
     1. 测试 `pm2 start dev.json`
     2. 正式 `pm2 start dev.json`
  3. 查看日志 `pm2 logs`

## 对应的客户端

* 目前就只做了 App 端,按理说目前接口基本可以做个网页前端的,微信公众号以及小程序,在做些修改也是应该可以的;

## 仓库地址

[服务器地址 GitHub 地址,具体配置看文档](https://github.com/strawferry/lostserver)

[App 地址,具体配置看文档](https://github.com/strawferry/lostapp)

# 个人博客
### **博客地址: [`https://cblog.ferryvip.com/`](https://cblog.ferryvip.com/)**