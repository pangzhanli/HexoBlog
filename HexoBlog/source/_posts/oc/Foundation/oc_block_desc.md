---
title: OC中的Block简单介绍
date: 2020-04-03 14:07:19
categories:
- OC
- Foundation
tags: OC
---


Block的意思就是 块，跟java中的匿名内部类的实现有点相似，例如：



 //定义了一个block,这个block返回值是int类型，接收两个int类型的参数

    int (^Sum)(int,int)=^(int a,int b){

        return a+b;

    };

    

    int a=Sum(10,5);

    

    NSLog(@"%i",a);



上述代码中，定义一个Block用 ^符号， Block有返回值类型，也可以有参数。

我们可以先定义一个Block类型，然后再去实现，例如：



    //定义了MySum这种Block类型

    typedef int (^MySum)(int,int);

    

   //定义了一个block变量

    MySum sum1=^(int a,int b){

        return a+b;

    };

    

    int c=sum1(1,2);

    NSLog(@"%i",c);

例如上边的代码中，先用typedef定义了一个叫MySum的Block类型，然后再定义一个block变量，最后在调用。



Block在使用的时候，跟指针函数有点类似，例如：



int sum(int a,int b){

    return a+b;

}





void test(){

    //block

    int (^Sum)(int,int)=^(int a,int b){

        return a+b;

    };

    int c=Sum(10,10);

    NSLog(@"%i",c);





    //指针函数

    int (*sump)(int ,int)=sum;

    

    c=(*sump)(10,7);

    NSLog(@"%i",c);

}