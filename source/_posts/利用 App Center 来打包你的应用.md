---
title: 利用 App Center 来打包你的应用
date: 2019-05-07 16:26:34
tags:
---
# 利用 App Center 来打包你的应用
App Center 是巨硬(微软)家的一个应用开发管理平台服务,之前主要使用的是他的 CodePush 服务,后续平台升级了,把开发的崩溃收集,数据统计,推送服务,应用构建及测试,CodePush 等多个服务融合在一起,做出的 App Center 平台,基本功能也都是免费的,今天这篇文章主要是讲 iOS (原生和 ReactNative)应用通过 App Center 来打包;

## 0. 前期准备
1. App Center 账号(可通过 GitHub 账号授权登录) [https://appcenter.ms](https://appcenter.ms);
2. GitHub 账号 [https://github.com/](https://github.com/);

## 1. 设置 Build 配置

### 1.1 仪表盘点击创建应用
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2sptw03wnj220k0y00xn.jpg)

### 1.2 填写应用信息
> 1. 填写应用基础信息  --> 应用名称 --> Release type
> 2. App Center 可以用来构建多种系统平台的应用,以及不同平台写的应用
> 3. 这边我们 OS 选取 iOS , Platform 选 Objective-C / Swift

![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2spvcr5lgj221e11eq9v.jpg)

### 1.3 添加构建仓库
> 点击构建配置,连接仓库,选取 GitHub 仓库

![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2sq5x2f1vj222a116dmg.jpg)
> 通过关联的 GitHub 账号,选取相应的 iOS 仓库

![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2sq7ty51vj2226114wlv.jpg)
### 1.4 分支构建配置
> 根据 GitHub 仓库获取仓库分支,点击分支对应的构建配置

![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2sq9bl4vpj223u0ys43f.jpg)
### 1.5 构建配置
> 1. App Center 会读取仓库的文件,让你选取你要构建的 Project/Workspace 和相应 Shared Scheme;
> 2. Xcode 版本;
> 3. Build scripts 自定义构建脚本,脚本是包含在 git 仓库文件里,具体配置[见文档](https://docs.microsoft.com/en-us/appcenter/build/custom/scripts/);(可选配置)
> 4. 构建触发规则, push 触发构建/手动触发;
> 5. 自动增加构建号,自动测试配置;(可选配置)
> 6. 环境变量设置,[见文档](https://docs.microsoft.com/en-us/appcenter/build/custom/variables/)
> 7. 签名证书设置,证书导出这边不做过多介绍,可参考[链接](https://www.jianshu.com/p/96ce1201b32e);
> 8. 真机测试,分发构建,构建状态图标;(可选配置)

![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2sqc4f8bbj223g2b4kaa.jpg)

### 1.6 分支构建历史
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2sr1apnj3j221019ggsk.jpg)
### 1.7 构建产物
> 构建完成后有 ipa 包等,可以通过 App Center 分发

![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2sraxze93j221s1a2k4v.jpg)
> 但是个人发现访问和下载速度上不是很快,所以通过 Post-build 脚本自己上传到蒲公英托管平台;

```bash
#!/usr/bin/env bash

if [ "$AGENT_JOBSTATUS" == "Succeeded" ]; then

ukey=蒲公英ukey
apikey=蒲公英apikey
desc=蒲公英上传描述

curl -F "file=@$APPCENTER_OUTPUT_DIRECTORY/$APPCENTER_XCODE_SCHEME.ipa" \
 -F "uKey=$ukey" -F "_api_key=$apikey" \
  -F "updateDescription=$desc" https://qiniu-storage.pgyer.com/apiv1/app/upload

fi
```

![](https://ws1.sinaimg.cn/large/8bbf0afbly1g2st0ejwiqj216s0o8adx.jpg)

## 2. 总结
App Center 里面提供了一系列的关于应用开发的 SDK 和服务,产品做得很全面,还提供了一些云的概念操作(线上打包);

有时间可以多研究 App Center 的这一套东西,如果一个公司规模够大,产品丰富,也可以自己搭建一个自己像这样的一套系统;