---
title: 08-sqlite字段更名
toc: true
date: 2020-11-18 19:41:29
tags: sqlite
categories:
- OC
- sqlite
---


提出问题： 当模型类的属性由age更改为age2的时候，在更新数据的时候，如何将老表中的age更新到对应的age2中？

1，给XMGModelProtocol协议添加映射方法：

![](08-sqlite字段更名/08_001.png)

2，模型类运用：

![](08-sqlite字段更名/08_002.png)

实现类中：

![](08-sqlite字段更名/08_003.png)

3，修改XMGSqliteModelTool工具类中的updateTable:uid: 方法

![](08-sqlite字段更名/08_004.png)
