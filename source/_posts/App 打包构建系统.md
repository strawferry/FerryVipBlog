---
title: App 打包构建系统
date: 2019-06-03 16:26:34
tags:
---

# App 打包构建系统
## 0. 由来
根据开发测试等实际应用需求设计了一套打包构建系统,系统包括以下主要功能:
1. App 多环境打包;
2. App 自动发布热更新;
3. App 管理托管;

---

系统的基本组成:

1. 通过 Jenkins 来做打包,热更新推包,自动测试服务;
2. 应用打包完成上传到蒲公英,并把蒲公英上的下载地址等信息通过自建的 Node 服务做应用的托管,这样我们就可以在 Node 中对应用做相应的管理操作;
3. 热更新推包后,我们记录相应的数据后,也记录到 Node 服务中,这样我们也可以在 Node 服务中对热更新做出查看或者撤回更新等操作;


> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g540zcsjwrj22aw1akjzc.jpg)


## 打包对比
**手动打包 VS 自动打包**

|     手动打包     |       自动打包      | 
|:---------------:|:-----------------:|
|   耗时长,效率低;  | 自动化打包,解放双手; | 
|重复性多,人工成本高;| 配置好后,一键操作;   | 
|     出错性概率大; | 可配置一键远程打包;  | 


## 1. 主要功能点

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g540zcc9ggj22b41b079q.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g540zd6a0vj22as1ag43c.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g540zdcck5j22as1aejwy.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g540zd226hj22ay1ag447.jpg)
![](https://ws1.sinaimg.cn/large/8bbf0afbly1g540zcz0t8j22aq1aoq9k.jpg)

## 2. 主要实现点

> ![](https://ws1.sinaimg.cn/large/8bbf0afbly1g540zd2vfnj22ao1asai0.jpg)

