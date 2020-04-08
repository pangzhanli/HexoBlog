---
title: C语言中枚举的简单介绍
date: 2020-04-03 14:26:49
categories: C语言
tags: C
---

1,枚举是C语言中一种基本数据类型，可以用于声明一组常数。当一个变量有几个固定的可能取值时，可以将这个变量定义为枚举类型。比如可以用枚举来表示季节，春天，夏天，秋天，冬天。

2,定义形式：

enum 枚举名称 {元素1，元素2，元素3，...};

例如： enum Season {spring,summer,autumn,winter};

3,枚举变量的定义有3种方式

a,先定义枚举类型，再定义枚举变量

enum Season {spring,summer,autumn,winter};

enum Season s;

b,定义枚举类型的同时定义枚举变量

enum Season {spring,summer,autumn,winter}  s;

c,省略枚举名称，直接定义枚举变量

enum {spring,summer,autumn,winter} s;

使用以上3中方式中的任何一种方式都是可以的。

4，基本操作

a,赋值操作



enum Season {spring, summer, autumn, winter} s;

s = spring; // 等价于 s = 0;

s = 3;//等价于 s = winter;

b,遍历



enum Season {spring, summer, autumn, winter} s;

// 遍历枚举元素

for (s = spring; s <= winter; s++) {

    printf("枚举元素：%d \n", s);

}

输出结果 ， 0 ，1，2，3
