---
title: 使用 GitLab-CI 和 GitLab Runner 打包 iOS 应用
date: 2019-08-08 11:26:34
tags:
---
# 使用 GitLab-CI 和 GitLab Runner 打包 iOS 应用

## 折腾由来
来源于一篇国外的[博客 iOS Continuous Integration with GitLab CI, Fastlane & OTA Installation](https://medium.com/flawless-app-stories/ios-continuous-integration-with-gitlab-ci-fastlane-and-ota-installation-from-gitlab-pages-f312e07ab06e),看到其使用 GitLab-CI 和 GitLab Runner 来打包 iOS 应用做持续集成,看着还不错,自己之前也做了一些持续集成的例子;



## 1. [安装 runner](https://docs.gitlab.com/runner/install/)
* 手动安装(推荐)
	1. 下载 binary `sudo curl --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-darwin-amd64`
	2. 设置权限 `sudo chmod +x /usr/local/bin/gitlab-runner`
* brew 安装(发现会有权限问题)
	1. 安装 `brew install gitlab-runner`
	2. 启动 `brew services start gitlab-runner`

## 2. [注册 Runners](https://docs.gitlab.com/runner/register/index.html)

```
1. 注册 runner
sudo gitlab-runner register
2. 填写 gitlab-ci 地址,这边以官方的为主
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com )
https://gitlab.com
3. 输入获取的 token ,下面会介绍如何获取
Please enter the gitlab-ci token for this runner
xxx
4. 输入描述,后面可以修改
Please enter the gitlab-ci description for this runner
mac description
5. 输入机器的 tag,后面可以修改
Please enter the gitlab-ci tags for this runner (comma separated):
mymac
6. 输入执行类型,这边填入 shell
Please enter the executor: ssh, docker+machine, docker-ssh+machine, kubernetes, docker, parallels, virtualbox, docker-ssh, shell:
docker
shell
```

![获取 token](https://ws1.sinaimg.cn/large/8bbf0afbly1g5s3nzlhr8j221a28gay4.jpg)

## 3. [配置 .gitlab-ci.yml 文件](https://gitlab.com/help/user/project/pipelines/settings#custom-ci-config-path)

在 git 的根目录创建 `.gitlab-ci.yml ` 文件,内容示例如下

```yml

before_script:
  - echo "----------global---before_script--------------"

stages:
  - build
  - publish
# 构建 pipeline

build_job:
  stage: build
  tags:
    - testmac
  before_script:
    - echo "------build-------before_script--------------"
  script:
    - sh ios.sh
# 打包 App 脚本
  artifacts:
    expire_in: 90 days
    paths:
      - build
# 构建产物打包保存服务器
  only:
    - master

pages:
  stage: publish
  script:
    - ls build
index.html
  artifacts:
    expire_in: 90 days
    paths:
      - build
# 把 build 文件设置成 pages 静态托管
  only:
    - master
```
[一些 gitlab-ci 配置文档, GitLab CI/CD Pipeline Configuration Reference](https://docs.gitlab.com/ee/ci/yaml/README.html)

## 4. 自动构建
当代码推上去后, gitlab-ci 会触发构建,向 GitLab Runner(自己设置的机器) 发布任务,并执行构建

* push 取消自动构建

```
git push --push-option=ci.skip    # using git 2.10+
git push -o ci.skip               # using git 2.18+
```
![构建面板](https://ws1.sinaimg.cn/large/8bbf0afbly1g5s3nxzvb3j22741n4arj.jpg)
## 5. 定时自动构建
根据自己需要自己添加定时构建
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g5s41sx3bpj22721muai3.jpg)