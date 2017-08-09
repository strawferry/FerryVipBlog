---
title: 利用 Travis CI 自动部署 hexo 博客到 GitHub Pages 上
date: 2017-04-16 17:26:34
tags:
---

最近一直在看一些关于持续集成的东西,持续集成会对整个项目的敏捷开发有很大的帮助;

了解过 jenkins, 功能非常强大,但是在做 iOS 持续集成必须在一台 Mac 系统下,后面通过了解和别人介绍,认识到了今天的主角 Travis CI;

hexo虽然可以方便地部署github静态博客，但是仅仅是把最终生成的html保存在repository中，像原始的Markdown文件，hexo配置文件，主题配置文件，修改文件都仅仅是保存在本地。这样不利于保存，也无法查看每篇博客的修改历史。更重要的是无法做到跨平台，也不易于多人写作。

想法是每次写博客，只需要push md文件及博客所需的资源文件即可。Travis CI持续集成tool可以满足此需求。

Travis CI 目前主要是和 GitHub 一起使用,所以今天的例子就以 hexo 博客的每次 push 触发 Travis CI 自动部署到 GitHub 的 Pages 上;

## 1. 思路
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1feoojwv4fej20r20cpwje.jpg)

## 2. 具体实现

### 2.1 首先需要在 GitHub 上面创建一个仓库(或者已有)

>以新建仓库为例

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1feoow4xyehj20ke0esad6.jpg)

### 2.2 生成 Personal Access tokens
> 为后续的功能生成的 token

登录github, settings -> Personal access tokens -> Generate new token

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1feoow57epmj21nk1a4n60.jpg)

填写token description，比如叫 travis.并勾选上授予的权限，比如我勾选的是repo和gist，然后create.

>![](https://ws1.sinaimg.cn/large/8bbf0afbly1feoow4xvs2j20l60e0tci.jpg)

将产生的token串复制保留下来，后面会使用到,如果丢失，只能重新产生。

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1feoow4xzrej20l50aujvg.jpg)

### 2.3 [travis-ci 设置](https://travis-ci.org/)
登录 travis-ci 网站,利用 GitHub 账号登录;

同步 GitHub 仓库
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1feopcj6xuqj20ug0ctjv3.jpg)

选取刚才创建的仓库并打开
>![](https://ws1.sinaimg.cn/large/8bbf0afbly1feopcj4vwfj20d808fgmt.jpg)

添加刚才的 token 作为全局变量
>![](https://ws1.sinaimg.cn/large/8bbf0afbly1feopcj8aw7j20v60ql7b3.jpg)

### 2.4 [hexo 博客设置](https://hexo.io/)

基本的 hexo 命令

```bash
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
进入 blog 所在的文件夹下，新建 `.travis.yml` 文件，并添加以下内容

```javascript
# 使用语言
language: node_js
# node版本
node_js: stable
# 设置只监听哪个分支
branches:
  only:
  - source
# 缓存，可以节省集成的时间，这里我用了yarn，如果不用可以删除
cache:
  apt: true
  yarn: true
  directories:
    - node_modules
# tarvis生命周期执行顺序详见官网文档
before_install:
- git config --global user.name "name"
- git config --global user.email "mmail@mail.com"
# 由于使用了yarn，所以需要下载，如不用yarn这两行可以删除
- curl -o- -L https://yarnpkg.com/install.sh | bash
- export PATH=$HOME/.yarn/bin:$PATH
- npm install -g hexo-cli
install:
# 不用yarn的话这里改成 npm i 即可
- yarn
script:
- hexo clean
- hexo generate
after_success:
- cd ./public
- git init
- git add --all .
- git commit -m "Travis CI Auto Builder"
# 这里的 REPO_TOKEN 即之前在 travis 项目的环境变量里添加的
- git push --quiet --force https://$REPO_TOKEN@git@github.com/strawferry/FerryVipBlog.git master
```
然后，准备 push 该项目到 github ，如果是新项目可参照下面的git指令

```bash
git init
# 添加自己的项目
git remote add origin git@github.com:strawferry/travis.git
# 新建并切换分支
git checkout --orphan source
git add -A
git commit -m "init repo"
git push
```
### 2.5 发布博客文章

```bash
前往 source 分支下:
hexo new title   // 1. 新建文章;
2. 使用 markdown 软件或者 vim 直接编写文章内容,并保存文件;
3. 把目前分支的内容变化提交到 git 线上仓库;
4. 接着就等待 travis-ci 自动部署到 pages 上;
```
![](https://ws1.sinaimg.cn/large/8bbf0afbly1feouarcga0j20uy0sqn63.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1feouaresa4j20mx0s0k4r.jpg)

这样你的博客就已经成功部署到 pages 上面了

## 总结
这个是一个简单的对 travis-ci 的入门,这样能够给我们提供不少的事,持续集成能够给开发带来极大的便利,让程序员不做一些重复的事情,提高效率;