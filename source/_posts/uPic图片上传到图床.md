---
title: uPic图片上传到图床
date: 2020-09-24 13:26:34
tags:
---

之前写文章用的图床是在微博,后面发现微博把这个给封了,这就让人很尴尬,最主要问题就是图片没了,之前的文章图片也没有备份,只能找寻新的图床,后面找到了 [uPic](https://github.com/gee1k/uPic) 软件,开源的用着也还不错,主要是可以上传图片到 git 仓库,还有外链,图片还能备份,满足了我基本使用,今天的文章就是 [uPic](https://github.com/gee1k/uPic) 和 [gitee](https://gitee.com) 配合的基本配置;

## 1. uPic 软件下载

[https://github.com/gee1k/uPic/releases](https://github.com/gee1k/uPic/releases) GitHub 去下载最新版本的文件,解压缩托进应用程序文件夹,双击打开就可使用

## 2. gitee 配置
1. 新建仓库

> ![16-19-zNF3dd-gitee仓库创建](https://cdn.jsdelivr.net/gh/strawferry/GSS@master/uPic/2020-09-24/16-19-zNF3dd-gitee%20%E4%BB%93%E5%BA%93%E5%88%9B%E5%BB%BA.jpg)

2. Token 创建
	* 1. 进入[码云 Token 创建页面](https://gitee.com/profile/personal_access_tokens/new)
	* 2. 勾选 repo 访问权限。然后滚动页面到底部，点击Generate token按钮来生成 token
	> ![16-19-J68X4y-Token生成1](https://cdn.jsdelivr.net/gh/strawferry/GSS@master/uPic/2020-09-24/16-19-J68X4y-Token%E7%94%9F%E6%88%901.jpg)
	* 3. 复制生成好的 Token 值到 uPic token 输入框
	![16-19-hkrtd9-Token生成2](https://cdn.jsdelivr.net/gh/strawferry/GSS@master/uPic/2020-09-24/16-19-hkrtd9-Token%E7%94%9F%E6%88%902.jpg)
	**注意：**此 Token 只会显示一次！请务必保存好，否则之后丢失了，就得重新创建

## 3. uPic 软件配置
打开 `uPic` 的偏好设置,选择图床,添加 `Gitee` 图床,输入我们刚才创建的仓库资料和 `Token`,配置完成可以点击验证,看是否能够成功;

保存路径我是设置为 `uPic/{year}-{month}-{day}/{filename}-{hour}-{minute}-{random}{.suffix}`
---
> ![16-19-z3yzaa-uPic设置](https://cdn.jsdelivr.net/gh/strawferry/GSS@master/uPic/2020-09-24/16-19-z3yzaa-uPic%E8%AE%BE%E7%BD%AE.jpg)
---
> ![16-19-4fmCAf-uPic上传设置](https://cdn.jsdelivr.net/gh/strawferry/GSS@master/uPic/2020-09-24/16-19-4fmCAf-uPic%E4%B8%8A%E4%BC%A0%E8%AE%BE%E7%BD%AE.jpg)
---

## 4. uPic 软件使用
一般使用的话我是选择文件上传
---
> ![16-19-q8z5tJ-uPic选取文件](https://cdn.jsdelivr.net/gh/strawferry/GSS@master/uPic/2020-09-24/16-19-q8z5tJ-uPic%E9%80%89%E5%8F%96%E6%96%87%E4%BB%B6.jpg)
---

还有一个是拖拽文件直接上传
> ![16-19-8WcCLu-uPic拖拽文件上传](https://cdn.jsdelivr.net/gh/strawferry/GSS@master/uPic/2020-09-24/16-19-8WcCLu-uPic%E6%8B%96%E6%8B%BD%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0.gif) 
> 
