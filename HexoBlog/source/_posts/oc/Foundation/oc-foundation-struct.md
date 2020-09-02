---
title: Foundation中结构体的简单介绍
date: 2020-04-03 14:30:33
categories:
- OC
- Foundation
tags: Foundation
---

一：先看一下，在c语言中定义的结构体：



    //定义了Date这种结构体类型

    struct Date{

        int year;

        int month;

        int day;

    };

    //定义结构体变量

    struct Date d={2014,7,4};

    

   NSLog(@"year is %i,month is %i,day is %i",d.year,d.month,d.day);

   d.day=6;

   NSLog(@"day is %i",d.day);



如上事例中的



struct Date{

        int year;

        int month;

        int day;

    };

定义了一个结构体类型。

定义变量时：

struct Date d={2014,7,4};

使用：d.year,d.month,d.day



我们也可以使用typedef来定义一个结构体类型：如：



    typedef struct {

        int year;

        int month;

        int day;



    } MyDate;

    MyDate d={2014,7,4};

    NSLog(@"year is %i,month is %i, day is %i",d.year,d.month,d.day);

二：Foundation中的结构体
Foundation常用的结构体有：NSRange,NSPoint,NSSize,NSRect

1,NSRange的介绍：
我们先看一下，在NSRange.h中，NSRange的定义：
typedef struct _NSRange {

    NSUInteger location;

    NSUInteger length;

} NSRange;


这个结构体用来表示事物的一个范围，通常是字符串里的字符范围或者集合里地元素范围。其中，location表示该范围的起始位置，length表示该范围内所含的元素个数。
比如，在 "I Love You" 中，Love可以用location为2，length为4的范围来表示。
NSRange创建方式有3种：
a,  第一种，直接给成员变量赋值
    
    NSRange range;

    range.location=10;

    range.length=4;

b, 第二种，应用c语言的聚合结构赋值机制

   

    NSRangerange={8,3};

c, 第三种，应用Foundation框架提供的一个快捷函数NSMakeRange

    NSRange range=NSMakeRange(12,3);

使用，可以直接通过调用变量名引用，也可以将变量转换成字符串输出，比如：

通过变量名称引用：



NSLog(@"location is %zi",range.location);//其中z代表无符号

将变量转换成字符串输出，调用了NSString中的一个函数 NSStringFromRange



NSString *str=NSStringFromRange(range);

2,NSPoint的介绍：



先看一下NSPoint的定义：
   struct CGPoint {

     CGFloat x;

     CGFloat y;

   };

   typedef structCGPoint CGPoint;

其中CGPoint和NSPoint是相等的

这个结构体代表的时平面中的一个点（x,y）

创建方式有3种：
a,直接赋值
    NSPoint p;

    p.x=8;

    p.y=10;

b,调用NSMakePoint函数创建

NSPoint p=NSMakePoint(3, 5);


c,调用CGPointMake函数创建

NSPoint p=CGPointMake(6,8);
使用：
NSString *str=NSStringFromPoint(p);

3,NSSize的介绍：

先看一下NSSize的定义：
   struct CGSize {

      CGFloat width;

      CGFloat height;

   };

   typedef structCGSize CGSize;

其中CGSize和NSSize是相等的
这个可以用来代表布局，或者是一个按钮的宽度和高度。

创建方式有3种：
a,直接赋值

    NSSize size;

    size.width=100;

    size.height=80;


b,调用NSMakeSize函数来创建
NSSizesize=NSMakeSize(50,60);

c,调用CGSizeMake函数来创建

NSSizesize=CGSizeMake(40,50);

使用: 
NSString *str=NSStringFromSize(size);

4,NSRect的介绍：
先看一下NSRect的定义：
struct CGRect {

  CGPoint origin;

  CGSize size;

};

typedef structCGRect CGRect;

其中CGRect和NSRect是一样的
这个结构体用来存储宽度和高度以及横坐标和纵坐标

a,直接赋值
    NSRect rect;

    rect.size.height=8;

    rect.size.width=10;

    rect.origin.x=40;

    rect.origin.y=50;

b,调用NSMakeRect函数创建
    NSRect rect=NSMakeRect(100,80,10,8);

c,调用CGRectMake函数创建

    NSRect rect=CGRectMake(100,80,10,8);

使用：
    NSString *str=NSStringFromRect(rect);