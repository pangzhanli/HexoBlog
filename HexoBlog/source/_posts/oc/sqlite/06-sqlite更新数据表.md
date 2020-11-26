---
title: 06-sqlite更新数据表
toc: true
date: 2020-11-18 19:40:44
tags: sqlite
categories:
- OC
- sqlite
---


1，创建XMGTableTool工具类，获取所有排序以后所有的列名。

![](06-sqlite更新数据表/06_001.png)

实现方法：

![](06-sqlite更新数据表/06_002.png)

![](06-sqlite更新数据表/06_003.png)


2， 在XMGModelTool工具类中，添加获取排序后的所有字段对应到数据库的名称

![](06-sqlite更新数据表/06_004.png)

实现方法：

![](06-sqlite更新数据表/06_005.png)


3，在XMGSqliteModelTool工具类中，添加表是否要更新的方法：

![](06-sqlite更新数据表/06_006.png)

实现方法：

![](06-sqlite更新数据表/06_007.png)

