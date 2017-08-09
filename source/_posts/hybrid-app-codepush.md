---
title: 混合app集成热更新
date: 2017-02-22 15:55:02
tags: 
---

# 混合app集成热更新
原因是因为之前做的都是纯 rn 项目,偶尔接入原生,所以 codepush 比较好集成.

有一次在想如果原本是原生的项目,后面只是引入 rn 作为一些基础模块,这样的更新要如何做,也就有了这篇文章(技术很早实现了,博客因为懒后面盆友需要,拖了现在才写,也是尴尬);

## 1. 前提工作

你目前的 iOS 项目已经是 ReactNative 混合 App;
这边我用我之前的来做,具体代码可以看[这个链接(国内Coding)](https://ferryvip.coding.me/FerryVipBlog/2016/12/28/iOS-with-ReactNative/)或者[这个链接(国外github)](https://strawferry.github.io/FerryVipBlog/2016/12/28/iOS-with-ReactNative/);

## 2. 了解一些 codepush 的原理

之前在 CSDN 写的 codepush 相关的博客

[CodePush 热更新ReactNative之CodePush CLI操作](http://blog.csdn.net/strawferry/article/details/52124362)

[CodePush 热更新ReactNative之React Native Client SDK](http://blog.csdn.net/strawferry/article/details/52130870)

可以看下了解,当然最好去[官方 gayhub 去看文档](https://microsoft.github.io/code-push/index.html)比较好;

按照文档吧 codepush 的环境安装好👌;

## 3. 集成进入 App 项目里
1. 安装 codepush 模块 `npm install --save react-native-code-push@latest`;
2. 在安装完成后,可以执行命令自动导包进去 `react-native link react-native-code-push`, 当然也可以手动导包,自己[看下官方文档](https://github.com/Microsoft/react-native-code-push/blob/master/docs/setup-ios.md);
在自动导包时,会要求你添加 codepush 的 key, 可以跳过下面会说到怎么添加;
3. 到此就可以看到 package.json 里面多了一个模块;
目录变化
![目录变化](https://ws1.sinaimg.cn/large/8bbf0afbly1fczbmb0flej20hp0aftbz)

原生项目文件变化,添加了 CodePush 工程,还有一些静态库,至于 AppDelegate.m 里面的好像是会有,有点忘记了;
![原生项目文件变化](https://ws1.sinaimg.cn/large/8bbf0afbly1fczbxpo37qj20qs0lqk2g)

## 4. 配置 codepush 的 key

1. codepush 创建 app `code-push app add MyApp-iOS` 会从中得到一个 key ,复制这个 key ,下一步在 iOS 原生中会用到;
![key](https://ws1.sinaimg.cn/large/8bbf0afbly1fczc7np6mwj20pp0ezakd)
2. iOS中原生配置 key ,在 Info.plist 文件中,如下图;
![](https://ws1.sinaimg.cn/large/8bbf0afbly1fczcaop98uj20qs0lq7dn)

## 5. 原生代码配置
1. AppDelegate.m 文件中配置,为了一进入 App 就加载好了, codepush 环境,我个人认为的,没有去测试;
![](https://ws1.sinaimg.cn/large/8bbf0afbly1fczcl67242j20vn0v4wvj)
2. 在每处用到混合的地方加入代码,这边我用到了两处,所以两个的 .m 文件中,我都加入类似的代码;
![](https://ws1.sinaimg.cn/large/8bbf0afbly1fczclg4mmqj20vn0v4n94)

## 6. js 代码的配置
js 基本的配置就是这些,具体的有些配置,可以[官方文档看下](https://github.com/Microsoft/react-native-code-push/blob/master/docs/api-js.md);
![](https://ws1.sinaimg.cn/large/8bbf0afbly1fczcq1yucej20wz0cl7a8)

## 7. iOS 打 release 包
1. 在 js 主目录下,执行命令 `curl http://localhost:8081/index.ios.bundle -o main.jsbundle` 会在目录下有个 main.jsbundle 的文件,这个需要拖到 iOS 原生目录下,每次打包重新生成,都需要替换进去;
![](https://ws1.sinaimg.cn/large/8bbf0afbly1fczd173ncnj20rd0ign3j)
2. iOS 打包 ipa 包,只要把刚才的 main.jsbundle 拖进去,剩下的步骤和正常打包一样;
## 8. 打 codepush 更新包
在 js 的目录下,执行命令 `code-push release-react youAppName ios`, 最简单命令,直接推到Staging;

## 9. 到此基本结束,根据你设置的更新条件, App 就会自动更新了;

















