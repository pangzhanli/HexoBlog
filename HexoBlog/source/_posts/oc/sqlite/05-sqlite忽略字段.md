---
title: 05-sqlite忽略字段
toc: true
date: 2020-11-18 19:40:28
tags: sqlite
categories:
- OC
- sqlite
---


1，在 XMGModelProtocol类中，定义要忽略的方法

![](05-sqlite忽略字段/05_001.png)

2，在XMGStu类中

![](05-sqlite忽略字段/05_002.png)


3，在XMGModelTool类中，获取所有的成员变量以及成员变量对应类型的时候，将要忽略掉的字段忽略掉

![](05-sqlite忽略字段/05_003.png)