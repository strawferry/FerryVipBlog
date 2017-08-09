---
title: 折腾Hexo
date: 2016-12-12 17:57:22
tags: ["hexo配置"]
---
## Hexo 博客的安装流程

### 1.  配置环境
因为本人是用 Mac 所以就以主要介绍 Mac 的环境为主;
#### 1.1 安装 Node 环境
> 作用：用来生成静态页面的

方法1. 直接上 [https://nodejs.org/](https://nodejs.org/) 官网下载安装

方法2. Homebrew 安装
[Homebrew](http://brew.sh/) 是 Mac 系统的包管理器，用于安装 NodeJS 和一些其他必需的工具软件。

首先, 安装 Homebrew;

``` bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

复制上面代码在终端里面运行,等待安装完毕;

接下来在用 Homebrew 安装 Node;


``` bash
brew install node
```

 复制上面代码在终端里面运行,等待安装完毕;

#### 1.2  [Github](https://github.com/) 或者 [Coding](https://coding.net) 账户都可以
> 作用：是用来做博客的远程创库、域名、服务器之类的，怎么与本地hexo建立连接等下讲。

### 2. 正式安装 Hexo
#### 2.1 安装 Hexo 的命令行工具


``` bash
npm install -g hexo
```

复制上面代码在终端里面运行,等待安装完毕;

#### 2.2 初始化博客

``` bash
hexo init 你的博客名
```

在终端中前往你要放置博客的文件夹位置, 运行上面代码,等待安装完毕;
#### 2.3 配置 Github 仓库
登录到你自己的 github 账号, 点击 new repository 开始创建仓库, 按照下面的填写你自己要的参数;
![创建仓库](https://ws4.sinaimg.cn/large/8bbf0afbgw1faodnclhivj20lr0hhwhx.jpg)
配置 github pages 页面, 点击 Settings , 在 GitHub Pages 中开启配置为主分支
![配置 github pages](https://ws2.sinaimg.cn/large/8bbf0afbgw1faodocx895j20l90gtdje.jpg)
#### 2.4 配置 Hexo 文件
打开 Hexo 创建的根目录下的 _config.yml 文件,主要配置如下
![_config.yml 文件](https://ws4.sinaimg.cn/large/8bbf0afbgw1faodmmnzjoj206a0ccgmb.jpg)

``` yml
# Site
title: you blog  // 你博客的名称标题
subtitle: // 你博客的小标题(选填)
description: 好好过一生 // 博客的描述,可以写短小的座右铭
author: FerryVip // 作者你的名字
language: zh-Hans // 设置博客的语音(选填,默认英文)
timezone: // 时区(选填)
```


``` yml
# Deployment
deploy:
  type: git  // 类型就填 git
  repo: git@github.com:strawferry/FerryBlog.git // 你的仓库地址,在配置 github 仓库成功后会有,可以用 HTTPS (需要输入密码登录)和 SSH(需要配置SSH) 
  branch: master // 默认主分支
```


``` bash
npm install hexo-deployer-git --save
```

复制上面代码在终端的 hexo 目录下里面运行,等待安装完毕;

#### 2.5 node 生成静态文件
> `hexo generate` 或者 `hexo g`

复制上面代码在终端的 hexo 目录下里面运行,等待运行完毕;
#### 2.6 本地运行查看

``` bash
hexo server
或者 
hexo s
```

复制上面代码在终端的 hexo 目录下里面运行,等待运行完毕, 显示通过访问 `http://localhost:4000/` 就可以预览博客;
![](https://ws2.sinaimg.cn/large/8bbf0afbgw1faodsdxgi6j20zl0u4wl0.jpg)
#### 2.6 上传博客文件到 github

``` bash
hexo deploy
或者 
hexo d
```


复制上面代码在终端的 hexo 目录下里面运行,等待运行完毕;
等待运行完毕基本就能访问刚才在 github 配置 pages 的链接了;
#### 2.7 编写你的博客

``` bash
hexo new "new article"
```

之后在source/_posts目录下面，多了一个new-article.md的文件。
你通过编辑 new-article.md 就可以写你的日记了;
#### 2.8 一些常用的命令
>  `hexo clean` // 清除文件
> 
>  `hexo generate` // 生成静态文件
> 
>  `hexo deploy` // 部署代码上去 
> 
>  `hexo new "文章标题"` // 创建新文章

### 3. 配置 Hexo 主题
官方默认主题你懂得,不怎么好看,果断自己换个,本人觉得 [next](https://github.com/iissnan/hexo-theme-next) 的主题还可以,这边就以配置这个主题举个栗子;
[官方使用文档](http://theme-next.iissnan.com/)

主题下载
> `git clone https://github.com/iissnan/hexo-theme-next themes/next`

复制上面代码在终端的 hexo 目录下里面运行,等待下载完毕;

主题更改

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape // 改为 next
```

## 到此基本配置 Hexo 和 主题更换已经都会了,要更好使用,还需要自己看下文档去详细配置;


# 说说之前配置遇到的一个坑, 前面我没有说到,就是要等大家都配置完了,大伙也会碰到的问题,在最后给大家说一下

![](https://ws4.sinaimg.cn/large/8bbf0afbgw1faoe9p3zvtj20zk0u0jx2.jpg)

就是在本地跑 `hexo server` 一切看起来都好好的,样式都没啥问题, 当去看 pages 的时候,发现样式惨不忍睹,这就对了,因为还有一个东西还没有配置;

```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.com  // 把你在 pages 配置的那个网址链接复制在这个地方就解决了
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```





