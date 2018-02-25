---
title: React/React Native 的ES5 ES6写法对照表
date: 2016-07-04 16:22:51
tags:
---

## React/React Native 的ES5 ES6写法对照表

###1. 模块引用
>ES5 `使用CommonJS标准，引入React包基本通过require进行`

```JavaScript
var React = require("react");
var {
    Component,
    PropTypes
} = React;  //引用React抽象组件

var ReactNative = require("react-native");
var {
    Image,
    Text,
} = ReactNative;  //引用具体的React Native组件
```
>ES6 `import写法更为标准`

```JavaScript
import React, { 
    Component,
    PropTypes,
} from 'react';
import {
    Image,
    Text
} from 'react-native';
//注意在React Native里，import直到0.12+才能正常运作。
```
###2. 导出单个类
>ES5 `一般通过 module.exports 来导出`

```JavaScript
var MyComponent = React.createClass({
    ...
});
module.exports = MyComponent;
//引用的时候也类似：
var MyComponent = require('./MyComponent');
```
>ES6 `通常用export default来实现相同的功能`

```JavaScript
export default class MyComponent extends Component{
    ...
}
//引用的时候也类似：
import MyComponent from './MyComponent';
```
###3. 定义组件
>ES5 `通过React.createClass来定义一个组件类`

```JavaScript
var Photo = React.createClass({
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});
```
>ES6 `通过定义一个继承自React.Component的class来定义一个组件类`

```JavaScript
class Photo extends React.Component {
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}
```
###4. 给组件定义方法
>ES5  `名字: function()`

```JavaScript
var Photo = React.createClass({
    componentWillMount: function(){

    },
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});
```
>ES6 `名字()`

```JavaScript
class Photo extends React.Component {
    componentWillMount() {

    }
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}
```
###5. 定义组件的属性类型和默认属性
>ES5 `属性类型和默认属性分别通过 propTypes 成员和 getDefaultProps 方法来实现`

```JavaScript
var Video = React.createClass({
    getDefaultProps: function() {
        return {
            autoPlay: false,
            maxLoops: 10,
        };
    },
    propTypes: {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    },
    render: function() {
        return (
            <View />
        );
    },
});
```
>ES6 `可以统一使用static成员来实现`

```JavaScript
class Video extends React.Component {
    static defaultProps = {
        autoPlay: false,
        maxLoops: 10,
    };  // 注意这里有分号
    static propTypes = {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    };  // 注意这里有分号
    render() {
        return (
            <View />
        );
    } // 注意这里既没有分号也没有逗号
}
```

###6. 初始化STATE
>ES5 `getInitialState: function() { return {key: value}; },`

```JavaScript
var Video = React.createClass({
    getInitialState: function() {
        return {
            loopsRemaining: this.props.maxLoops,
        };
    },
})
```
>ES6 `两种写法`

```JavaScript
//写法1
class Video extends React.Component {
    state = {
        loopsRemaining: this.props.maxLoops,
    }
}
//写法2 我们推荐更易理解的在构造函数中初始化（这样你还可以根据需要做一些计算)
class Video extends React.Component {
    constructor(props){
        super(props);
        this.state = {
            loopsRemaining: this.props.maxLoops,
        };
    }
}
```
###7. 把方法作为回调提供
>ES5 在ES5下，React.createClass会把所有的方法都bind一遍，这样可以提交到任意的地方作为回调函数，而this不会变化。但官方现在逐步认为这反而是不标准、不易理解的。

```JavaScript
var PostInfo = React.createClass({
    handleOptionsButtonClick: function(e) {
        // Here, 'this' refers to the component instance.
        this.setState({showOptionsModal: true});
    },
    render: function(){
        return (
            <TouchableHighlight onPress={this.handleOptionsButtonClick}>
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
});
```
>ES6 在ES6下，你需要通过bind来绑定this引用，或者使用箭头函数（它会绑定当前scope的this引用）来调用

```JavaScript
class PostInfo extends React.Component
{
    handleOptionsButtonClick(e){
        this.setState({showOptionsModal: true});
    }
    render(){
        return (
            <TouchableHighlight 
                onPress={this.handleOptionsButtonClick.bind(this)}
                onPress={e=>this.handleOptionsButtonClick(e)}
                >
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
}
```
>箭头函数实际上是在这里定义了一个临时的函数，箭头函数的箭头=>之前是一个空括号、单个的参数名、或用括号括起的多个参数名，而箭头之后可以是一个表达式（作为函数的返回值），或者是用花括号括起的函数体（需要自行通过return来返回值，否则返回的是undefined）。

```
// 箭头函数的例子
()=>1
v=>v+1
(a,b)=>a+b
()=>{
    alert("foo");
}
e=>{
    if (e == 0){
        return 0;
    }
    return 1000/e;
}
```
>需要注意的是，不论是bind还是箭头函数，每次被执行都返回的是一个新的函数引用，因此如果你还需要函数的引用去做一些别的事情（譬如卸载监听器），那么你必须自己保存这个引用

```
// 错误的做法
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused.bind(this));
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this.onAppPaused.bind(this));
    }
    onAppPaused(event){
    }
}
// 正确的做法
class PauseMenu extends React.Component{
    constructor(props){
        super(props);
        this._onAppPaused = this.onAppPaused.bind(this);
    }
    componentWillMount(){
        AppStateIOS.addEventListener('change', this._onAppPaused);
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this._onAppPaused);
    }
    onAppPaused(event){
    }
}
从这个帖子中我们还学习到一种新的做法：
// 正确的做法
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused);
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this.onAppPaused);
    }
    onAppPaused = (event) => {
        //把方法直接作为一个arrow function的属性来定义，初始化的时候就绑定好了this指针
    }
}
```
###8. ES6+带来的其它好处
>解构&属性延展

结合使用ES6+的解构和属性延展，我们给孩子传递一批属性更为方便了。这个例子把className以外的所有属性传递给div标签：

```JavaScript
class AutoloadingPostsGrid extends React.Component {
    render() {
        var {
            className,
            ...others,  // contains all properties of this.props except for className
        } = this.props;
        return (
            <div className={className}>
                <PostsGrid {...others} />
                <button onClick={this.handleLoadMoreClick}>Load more</button>
            </div>
        );
    }
}
//下面这种写法，则是传递所有属性的同时，用覆盖新的className值：
<div {...this.props} className="override">
    …
</div>
//这个例子则相反，如果属性中没有包含className，则提供默认的值，而如果属性中已经包含了，则使用属性中的值
<div className="base" {...this.props}>
    …
</div>
```







