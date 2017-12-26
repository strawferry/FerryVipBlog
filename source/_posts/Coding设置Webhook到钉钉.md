---
title: Coding设置Webhook到钉钉
date: 2017-08-16 11:22:51
tags:
---

# 起因

最近用着钉钉,突然发现有个神奇的功能叫 Webhook 机器人,里面有 `Github` 的机器人,然鹅竟然没有我一直在用的 **[Coding.net](https://coding.net)** 的机器人,这个不能忍,本着程序员自己动手丰衣足食的勤劳准则,想着就自己折腾弄一个玩玩;

因为自己只会点 `Node.js` 所以就做了个包,具体的看下面;

效果图

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1filid4rbgug21ka0w77hd.gif)

## 准备工作

找了一下两家的文档
>[Coding Webhook 文档](https://open.coding.net/webhooks/)

>[钉钉自定义机器人文档](https://open-doc.dingtalk.com/docs/doc.htm?spm=a219a.7629140.0.0.V8Wb2O&treeId=257&articleId=105735&docType=1)

大概原理就是,钉钉提供一个发送消息的 Webhook 地址给你,然后 Coding 家提供了一个给你填入 Webhook 的地址接口,当仓库有信息变化,就会给你这个地址接口发消息;然而钉钉没有做这个 Coding 的接口,所以不能提供 Coding 直接把消息发到钉钉上,所以只能自己搭个服务器,先把 Coding 的消息解析一下,在发给钉钉.基本原理就是这样,说的有点乱,哈哈;

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1filia2e2chj21pe15sjz0.jpg)

## 服务器

设置 Webhook 路由;

```js
const express = require('express'),
    bodyParser = require('body-parser'),
    CWD = require('./../index'),
    app = express();

// 一般都会设置 bodyParser ,需要用到; 
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());


// 设置 Webhook 路由,已经中间件 CWD
app.post('/webhook', CWD());

app.listen(5566, function () {
    console.log('Express server listening on port http://localhost:6666');
});
```
CWD 中间件;

```js
const request = require('request');
exports = module.exports = function (options) {
    return function CodingHookDingDing (req, res, next) {
        let event = req.headers['x-coding-event'],
            body = req.body;
            // 通过头文件的 event 事件判断传入的参数等,做相应的信息解析;
        switch (event){
            case "push":
                return Push(req, res, next); // 对 push 做解析
            case "ping":
                return res.json({
                    "token": "123",
                    "zen": "Coding！ 让开发更简单"
                });
            default:
                return res.json(body);
        }
    };
};

function Push(req, res, next) {
	/*-- 消息的解析拼接 --*/
    let body = req.body;
    let ding = body.token;
    let count = body.commits.length;
    let whopush = body.commits[0].committer.name;
    let repourl = `${body.repository.owner.web_url}/p/${body.repository.name}/git/tree/${getbranch(body.ref)}`;
    let branch = `# [[${body.repository.name}/${getbranch(body.ref)}]](${repourl})`;
    let text = `${branch} ${count} commit,push by ${whopush}\n ## commits:\n`;
    for (let i = 0; i < count; i++){
        let com = body.commits[i];
        let name = com.committer.name;
        let mes = com.short_message;
        let hash6 = com.sha.substring(0,6);
        let commit = `> </> ${name}: [[${hash6}]](${com.web_url})-${mes}\n`;
        text = text + commit;
    }
    console.log(text);
    /*-- 消息的解析拼接 --*/
    
    // 钉钉消息格式等 body 设置 
    let rqbody = {
        msgtype: "markdown",
        markdown: {
            title:"仓库有新的代码更新咯!",
            text: text
        }
    };
    
    let options = {
        url: ding,
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(rqbody) // 消息体内容
    };
	// request 向钉钉发送消息 Webhook
    request.post(options, (err, res, body)=>{
        if(!err && res.statusCode == 200){
            let info = JSON.parse(body);
            console.log(info);
        }
    });
    res.json({mes: 'ok'});
}
function getbranch(str) {
    let arr = str.split('/');
    return arr[arr.length-1];
}
```


## 配置
### 1. 首先钉钉群里设置自定义机器人
**1. 设置自定义机器人**
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1filid4pd50j20mv0n479k.jpg)

**2. 填入机器人名称**
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1filid4ortwj20ix0ffq46.jpg)

**3. 复制 webhook 地址,后面有用**
![](https://ws1.sinaimg.cn/large/8bbf0afbly1filid4omjxj20iy0ffmyo.jpg)
### 2. Coding 仓库 Webhook 设置
**1. 点击到要设置的仓库 Webhook 页面,点击新建 Webhook**
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1filid4p9tbj20yf0egq5j.jpg)

**2. url 填入服务器上要监听的地址, token 填入刚才钉钉复制的 Webhook 地址,以及选取底部的监听类型,至少要勾选 Push**
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1filid4qf5fj21a40qajwl.jpg)

**3. 如果配置顺利,在你以后每次仓库的变化,在钉钉上面都会收到消息提醒**
> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1filid4tw0uj20qo0v4wnh.jpg)

## npm 包
后面就干脆做了个 npm 包发布上去,目前只对 push 操作做消息发送,后续有时间在完善下其他操作;

> 安装

`npm i --save hookding`

> 使用方法

```js
    const CWD = require('hookding');

    app.post('/router', CWD());

```


## [本文参与 Coding 征文计划](https://coding.net/wow/stories/)