---
title: iOS-with-ReactNative
date: 2016-12-28 14:08:04
tags:
---

# 如何在现有的iOS项目中添加ReactNative混合开发

如果公司的项目之前是用原生, 现在想做混合开发并且选择ReactNative, 这篇会是一个基础的环境配置;

## 1. 开发环境准备

首先, 至少你已经搭建了 `React Native` 的[开发环境](http://reactnative.cn/docs/0.39/getting-started.html)在iOS平台上所需的一切依赖软件（比如npm）。

其次, [CocoaPods](http://cocoapods.org/) 包管理工具, 基本做iOS开发都有装, 如果没有, 那就百度一下😂;
## 2. 安装依赖包
React Native的植入过程同时需要React和React Native两个node依赖包。
![](https://ws2.sinaimg.cn/large/8bbf0afbjw1fb4ay3fky6j20hk0c70vj.jpg)
在你的原有的iOS目录的上一级目录创建一个包管理package.json文件;
>对于一个典型的React Native项目来说，一般package.json和index.ios.js等文件会放在项目的根目录下。而iOS相关的原生代码会放在一个名为ios/的子目录中,这里也同时放着你的Xcode项目文件（.xcodeproj）。

```
// package.json 文件内容
{
  "name": "NumberTileGame",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start"
  },
  "dependencies": {
    "react": "15.4.1",
    "react-native": "0.39.2"
  }
}

// 通过npm info react和npm info react-native 来查看当前的最新版本
```
> npm install   // 在 package.json 的当前目录下开启终端执行这段代码, 这些模块就会安装到 `node_modules/` 下;

## 3. React Native框架嵌入iOS
### Subspecs

在你开始把React Native植入到你的应用中之前，首先要决定具体整合的是React Native框架中的哪些部分。而这就是subspec要做的工作。在创建Podfile文件的时候，需要指定具体安装哪些React Native的依赖库。所指定的每一个库就称为一个subspec。

可用的subspec都列在[node_modules/react-native/React.podspec](https://github.com/facebook/react-native/blob/master/React.podspec)中，基本都是按其功能命名的。一般来说你首先需要添加Core，这一subspec包含了必须的AppRegistry、StyleSheet、View以及其他的一些React Native核心库。如果你想使用React Native的Text库（即<Text>组件），那就需要添加RCTText的subspec。同理，Image需要加入RCTImage，等等。
### Podfile
在 CocoaPods 的 Podfile 中指定我们所需要使用的组件。如果原生没有用过 CocoaPods 管理;
> //在iOS原生代码所在的目录中（也就是`.xcodeproj`文件所在的目录）执行：
 `pod init`

Podfile 会创建在执行命令的目录中。你需要调整其内容以满足你的植入需求。调整后的Podfile的内容看起来类似下面这样：

```
# target的名字一般与你的项目名字相同
target 'NumberTileGame' do

  # 'node_modules'目录一般位于根目录中
  # 但是如果你的结构不同，那你就要根据实际路径修改下面的`:path`
  pod 'React', :path => '../node_modules/react-native', :subspecs => [
    'Core',
    'RCTText',
    'RCTNetwork',
    'RCTWebSocket', # 这个模块是用于调试功能的
    # 在这里继续添加你所需要的模块
  ]

end
```
### Pod安装
创建好了Podfile后，就可以开始安装React Native的pod包了。
> `pod install`

## 4. 代码集成
### 原生代码集成
在要混合开发的页面, 加入如下代码

``` objc
// RNViewController 页面
- (void)viewDidLoad {
    [super viewDidLoad];
    
    NSURL *jsCodeLocation = [NSURL URLWithString:@"http://localhost:8081/index.ios.bundle?platform=ios"];
    RCTRootView *rootView = [[RCTRootView alloc] initWithBundleURL : jsCodeLocation
                         moduleName        : @"HybridApp"
                         initialProperties : @{@"page" : @"RN1"}  // 传入参数,用于定义那个页面或者一些数据传输
                          launchOptions    : nil];
    self.view = rootView;
}

```

### ReactNative代码集成
` index.ios.js ` js 代码的入口

``` javascript
'use strict';
import {AppRegistry} from 'react-native';
import App from './app';
AppRegistry.registerComponent('HybridApp', () => App);
// 注册模块
```
` app.js ` 在这边做页面判断,当然你也可以根据自己的需求去做调整

``` javascript
'use strict';

import React from 'react';
import RN1 from './ReactNative1';
import RN2 from './ReactNative2';

export default class App extends React.Component {
    render() {
        return (
            this.props['page'] == 'RN1' ? <RN1 />:<RN2 />
        );
    }
}
```
` ReactNative1.js ` 页面1

``` javascript
'use strict';

import React from 'react';
import {
    StyleSheet,
    Text,
    View
} from 'react-native';
export default class ReactNative1 extends React.Component {
    render() {
        return (
            <View style={styles.container}>
                <Text style={styles.highScoresTitle}>ReactNative1</Text>
                <View style={{height: 100, width: 100, backgroundColor: 'blue'}} />
            </View>
        );
    }
}
const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#FFFFFF',
    },
    highScoresTitle: {
        fontSize: 20,
        textAlign: 'center',
        margin: 10,
    }
});
```
` ReactNative2.js ` 页面2

``` javascript
'use strict';
import React from 'react';
import {
    StyleSheet,
    Text,
    View
} from 'react-native';
export default class ReactNative1 extends React.Component {
    render() {
        return (
            <View style={styles.container}>
                <Text style={styles.highScoresTitle}>ReactNative2</Text>
                <View style={{height: 100, width: 100, backgroundColor: 'red'}} />
            </View>
        );
    }
}
const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#FFFFFF',
    },
    highScoresTitle: {
        fontSize: 20,
        textAlign: 'center',
        margin: 10,
    }
});
```

[>>项目gayhub地址<<](https://github.com/strawferry/HybridApp)
效果展示

![](https://ws3.sinaimg.cn/large/8bbf0afbjw1fb4aykwmpyg20970gjgok.gif)