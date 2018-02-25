---
title: CodePush 基本安装
date: 2016-07-20 13:23:42
tags:
---

## 1.电脑安装CodePush环境
>1. 安装命令`cnpm install -g code-push-cli`
>
>2. 查看版本`code-push -v`
>
>3. 注册账号`code-push register`
>
>4. 登陆 `code-push login`
>
>5. 注销 `code-push logout`
>
>6. 列出 登陆的token `code-push access-key ls`
>
>7. 删除某个access-key `code-push access-key rm <accessKey>`

### CodePush一些app管理指令
>1. 增加app的指令 `code-push app add <appName>`
>
>2. 列出所有app `code-push app ls`
>
>3. 更名 `code-push app rename 旧名字 新名字`
>
>4. 删除 `code-push app rm 旧名字`

### CodePush app部署管理指令
>默认部署类型 Production  Staging，还可以自己加例如dev  alpha beta等
>
>1. 列出app的部署环境 `code-push deployment ls <appName>`
>
>2. 增加部署环境 `code-push deployment add <appName> <部署名字>`
>
>3. 重命名部署名字：`code-push deployment rename app名字 旧部署名字 新部署名字`
>
>4. 删除部署名字 `code-push deployment rm app名字 部署名字`
>
>5. 查看历史版本`code-push deployment history appName deploymentName`

## 1.CodePush 项目目录下安装
>npm install --save react-native-code-push@latest

## 2.iOS Setup
### 2.1推荐使用RNPM安装-React Native Package Manager 
>工具安装命令 `npm i -g rnpm`

>Run `rnpm link react-native-code-push`

[其他安装方法](https://github.com/Microsoft/react-native-code-push)

>react-native bundle --platform ios --entry-file index.ios.js --bundle-output main.jsbundle 
>
>code-push release newCPT react-native bundle --platform ios --entry-file index.ios.js --bundle-output main.jsbundl 1.0.0  [--deploymentName Staging] [--description 描述1.0.0] [--mandatory true] 


