---
title: 07-Realm关系
toc: true
date: 2020-10-15 20:48:48
tags: Realm
categories:
- OC
- Realm
---


1，一对一关系：

![](07-Realm关系/07_001.png)

测试数据：

![](07-Realm关系/07_002.png)

2：一对多关系：

![](07-Realm关系/07_003.png)

但是，要在Dog的类声明中：

![](07-Realm关系/07_004.png)

测试数据：

![](07-Realm关系/07_005.png)

3，反向关系：

在Dog类中，如何获取Dog所属的主人呢？

声明链接对象：

![](07-Realm关系/07_006.png)

同时要在Dog的类实现中，重写linkingObjectsProperties方法，指定反向关系

![](07-Realm关系/07_007.png)

测试数据：

![](07-Realm关系/07_008.png)

