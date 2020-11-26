---
title: 10-sqlite删除数据
toc: true
date: 2020-11-18 19:42:23
tags: sqlite
categories:
- OC
- sqlite
---


1，以主键为判断条件的删除:

在XMGSqliteModelTool类中，添加删除方法：

![](10-sqlite删除数据/10_001.png)

具体实现：

![](10-sqlite删除数据/10_002.png)

2，自定义删除条件

![](10-sqlite删除数据/10_003.png)

具体实现：

![](10-sqlite删除数据/10_004.png)

3，根据自定义关系：

![](10-sqlite删除数据/10_005.png)


![](10-sqlite删除数据/10_006.png)

具体实现：

![](10-sqlite删除数据/10_007.png)

![](10-sqlite删除数据/10_008.png)

4，自定义删除语句：

![](10-sqlite删除数据/10_009.png)

具体实现：

![](10-sqlite删除数据/10_010.png)

