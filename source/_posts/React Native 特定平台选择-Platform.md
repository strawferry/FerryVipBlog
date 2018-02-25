---
title: React Native 特定平台选择-Platform
date: 2016-06-26 15:12:31
tags:
---

###1. 特定平台扩展名
>React Native会检测某个文件是否具有.ios.或是.android.的扩展名，然后根据当前运行的平台加载正确对应的文件。
>假设你的项目中有如下两个文件：
>`BigButton.ios.js` 
> `BigButton.android.js`
> 这样命名组件后你就可以在其他组件中直接引用，而无需关心当前运行的平台是哪个。
`import BigButton from './components/BigButton';`

###2. 实用的方法是Platform.select()
```JavaScript
var { Platform } = React;
var styles = StyleSheet.create({
  container: {
    flex: 1,
    ...Platform.select({
      ios: {
        backgroundColor: 'red',
      },
      android: {
        backgroundColor: 'blue',
      },
    }),
  },
});
//上面的代码会根据平台的不同返回不同的container样式——iOS上背景色为红色，而android为蓝色。
这一方法可以接受任何合法类型的参数，因此你也可以直接用它针对不同平台返回不同的组件，像下面这样：
var Component = Platform.select({
  ios: () => require('ComponentIOS'),
  android: () => require('ComponentAndroid'),
})();
<Component />;
```

###3. 平台模块
React Native提供了一个检测当前运行平台的模块。如果组件只有一小部分代码需要依据平台定制，那么这个模块就可以派上用场。
```
import { Platform } from 'react-native';
var styles = StyleSheet.create({
  height: (Platform.OS === 'ios') ? 200 : 100,
});
//Platform.OS在iOS上会返回ios，而在Android设备或模拟器上则会返回android。
```

###4. 检测Android版本
```
//在Android上，平台模块还可以用来检测当前所运行的Android平台的版本：
import { Platform } from 'react-native';
if(Platform.Version === 21){
  console.log('Running on Lollipop!');
}
```

[摘自React Native CN](http://reactnative.cn/docs/0.28/platform-specific-code.html#content)

