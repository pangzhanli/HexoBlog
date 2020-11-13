---
title: 02-Realm保存指定模型
toc: true
date: 2020-10-15 20:49:25
tags: Realm
categories:
- OC
- Realm
---



1, 创建一个Stu模型类，创建的时候，继承于RLMObject类，不是NSObject类。创建的时候，如图：

![](02-Realm保存指定模型/02_001.png)

2，声明属性的时候，不用指定nonatomic, 直接指定类型即可，如图：

![](02-Realm保存指定模型/02_002.png)

3，创建Stu对象的时候，直接指定数据的方式有两种：

![](02-Realm保存指定模型/02_003.png)

在保存stu对象的时候，要先开始一个事务，添加到realm对象中，然后再提交事务即可：

![](02-Realm保存指定模型/02_004.png)

或者是： 直接通过block形式：

![](02-Realm保存指定模型/02_005.png)
