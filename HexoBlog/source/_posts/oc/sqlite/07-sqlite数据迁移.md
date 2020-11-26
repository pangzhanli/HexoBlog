---
title: 07-sqlite数据迁移
toc: true
date: 2020-11-18 19:41:01
tags: sqlite
categories:
- OC
- sqlite
---


1，在XMGSqliteModelTool类中，添加更新表数据的方法：

![](07-sqlite数据迁移/07_001.png)

具体实现：

![](07-sqlite数据迁移/07_002.png)

![](07-sqlite数据迁移/07_003.png)


2，在XMGSqliteTool类中，添加批量执行语句：

![](07-sqlite数据迁移/07_004.png)

具体实现：

![](07-sqlite数据迁移/07_005.png)
