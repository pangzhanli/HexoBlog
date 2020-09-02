---
title: Foundation中的NSMutableString的创建
date: 2020-04-03 14:41:37
categories:
- OC
- Foundation
tags: Foundation
---


NSMutableString是可变字符串，相当于java中的StringBuffer。

NSMutableString可以预先分配存储空间，如果存储空间不够，会自动分配，这样效率会比较高。

它的方法的简单介绍：

setString  : 设置字符串的内容

appendString : 拼接一个字符串

appendFormat : 拼接带有格式符的字符串

replaceCharactersInRange : 替换字符串

insertString ： 插入字符串

deleteCharactersInRange ：删除字符串

如下是代码示例：


``` 
    //预先分配10个数字的存储空间

    NSMutableString *str=[[NSMutableString alloc] initWithCapacity:10];

    //设置字符串的内容

    [str setString:@"1234"];

    

    //拼接一个字符串

    [str appendString:@"567"];

    

    //拼接一个字符串

    [str appendFormat:@"age is %i and height is %.2f",27,1.7f];

    

    //替换字符串

    NSRange range=[str rangeOfString:@"height"];

   // NSRange range=NSMakeRange(7, 3);

    [str replaceCharactersInRange:range withString:@"no"];

    

    //插入字符串

    [str insertString:@"abc" atIndex:2];

    

    //删除字符串

    range=[str rangeOfString:@"age"];

    [str deleteCharactersInRange:range];

    

    NSLog(@"%@",str);

        

    //释放对象

    [str release];
   
``` 