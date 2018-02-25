---
title: CodePush 热更新操作
date: 2016-07-20 15:41:01
tags:
---

因为[微软开源](https://microsoft.github.io/code-push/docs/cli.html)的这个做的还不错,所以拿来用了
### 1.   CodePush CLI安装
* 首先要安装[Node.js](https://nodejs.org/en/)
* CodePush CLI安装 : `npm install -g code-push-cli`

### 2. Account 账号管理
* 注册`code-push register`
![codePush注册页面](http://img.blog.csdn.net/20160804224117391)
一般可以使用github登录(建议),也可以注册微软的账号!
* 退出账号后可以用`code-push link`,进入页面
* 登录 `code-push login`
> 条状页面,通过上面的那些图登录
> ![选择登录方式](http://img.blog.csdn.net/20160804225819229)
> 
> ![登录的key](http://img.blog.csdn.net/20160804225840433)
> 
> ![输入key](http://img.blog.csdn.net/20160804225951309)
* 当前登录账号 `code-push whoami`
* 退出当前登录 `code-push logout`
* 显示在那些电脑上面登录过账号 `code-push session ls`
* 移除在某台电脑的登录 `code-push session rm <machineName>`

---
* 获取access-key不通过浏览器 `code-push access-key add "VSTS Integration"`
* 通过上面的key登录 `code-push login --accessKey <accessKey>`
* 设置key到期时间  `code-push access-key patch <accessKeyName> --name "new name" --ttl 10d`
*  登录`HTTPS_PROXY or HTTP_PROXY`安全的一些东西`code-push login --noProxy` `code-push login --proxy https://foo.com:3454`

### 3. App 管理
* 新建推送热更新的App `code-push app add <appName>`
> 建议是iOS和安卓版本分开创建
> `code-push app add MyApp-Android`
> `code-push app add MyApp-iOS`

* 对App进行改名字 `code-push app rename <appName> <newAppName>`
* 移除App `code-push app rm <appName>`
* 列出账号的所有App `code-push app ls`
* App 增加参与的管理者(一般少用) `code-push collaborator add <appName> <collaboratorEmail>` 
* 移除参与的管理者 `code-push collaborator rm <appName> <collaboratorEmail>`
* 列出所有的参与者 `code-push collaborator ls <appName>`
* 把自己的这个App管理权限转移给其他人 `code-push app transfer <appName> <newOwnerEmail>`
### 4. 开发环境管理
* 增加开发环境 `code-push deployment add <appName> <deploymentName>`
* 移除 `code-push deployment rm <appName> <deploymentName>`
* 换名字 `code-push deployment rename <appName> <deploymentName> <newDeploymentName>`
*  列出所有的开发环境 `code-push deployment ls <appName>`
* 列出所有的开发环境和对应access-key `code-push deployment ls <appName> --displayKeys 或者 -k`
![环境](http://img.blog.csdn.net/20160804231831147)
> Active 当前表示激活比例
> Total  总共多少
> Pending 处于未升级和不确定因素
> Rollbacks 回滚的数
> Rollout
> Disabled
### 5. [更新版本管理](https://microsoft.github.io/code-push/docs/cli.html#releasing-updates-react-native)
* 最简单的方法 `code-push release-react MyApp ios` `code-push release-react MyApp android`
* code-push release-react hxlivei ios -d "PrePush" --des "停车场"
>code-push release-react <appName> <platform>
[--bundleName <bundleName>]
[--deploymentName <deploymentName>]
[--description <description>]
[--development <development>]
[--disabled <disabled>]
[--entryFile <entryFile>]
[--mandatory]
[--plistFile <plistFile>]
[--plistFilePrefix <plistFilePrefix>]
[--sourcemapOutput <sourcemapOutput>]
[--targetBinaryVersion <targetBinaryVersion>]
[--rollout <rolloutPercentage>]

### 6. 其他
* 清除更新记录 `code-push deployment clear <appName> <deploymentName>`
![清除历史](http://img.blog.csdn.net/20160804232838412)