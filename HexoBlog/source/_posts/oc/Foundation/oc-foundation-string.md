---
title: Foundation框架中字符串的创建
date: 2020-04-03 14:40:07
categories: OC
tags: Foundation
---

我们先看一下，c语言中的字符串是如何定义的，例如：



char *s="this is a string"; //C语言中的字符串·

在Foundation框架中，字符串的创建有有很多种，我们简单地介绍几种

1，创建常量字符串，例如：



//这种方式创建出来的字符串是不需要释放的

NSString *str1=@"this is a string";



2，创建空字符串，然后给予赋值



//这种方式创建出来的字符串需要释放,因为手动alloc,所以需要手动release

NSString *str2=[[NSStringalloc] init];

str2=@"this is a string";

[str2 release];



3，通过字符串，创建字符串（需要手动释放）



//这种方式创建出来的字符串需要释放,因为手动alloc,所以需要手动release



NSString *str3=[[NSStringalloc] initWithString:@"this is a string"];

[str3 release];



4，通过字符串，创建字符串（不需要手动释放）

//使用对应的静态方法创建字符串，这样就不需要管理内存

NSString *str4=[NSStringstringWithString:@"this is a string"];



5，将c语言中的字符串转换成oc中的字符串（需要手动释放）



//通过c语言的字符串转换成oc的字符串

NSString *str5=[[NSStringalloc] initWithUTF8String:"this is a string"];

[str5 release];



6，将c语言中的字符串转换成oc中的字符串(不需要手动释放)



//使用静态方法创建字符串，不需释放内存

NSString *str6=[NSStringstringWithUTF8String:"this is a string"];



7，通过Format创建字符串（需要手动释放）

//因为alloc,所以，需要手动释放内存



NSString *str7=[[NSStringalloc] initWithFormat:@"My age is %i and height is %.2f",24,1.71f];

[str7 release];



8，通过Format创建字符串（不需要手动释放）



//因为使用静态方法创建字符串，所以不需要手动释放

NSString *str8=[NSStringstringWithFormat:@"My age is %i and height is %.2f",24,1.71f];



9，我们还可以从磁盘上的文件中读取内容来创建字符串
//文件路径

NSString *path=@"/Users/mac/Desktop/test.txt";

//这个方法已经过期，只能解析英文内容，不能解析中文内容

NSString *str=[NSStringstringWithContentsOfFile:path];



10，通过指定字符串编码来创建字符串



NSError *err=nil;

//指定字符串编码为UTF-8   NSUTF8StringEncoding

NSString *str=[NSStringstringWithContentsOfFile:path encoding:NSUTF8StringEncodingerror:&err];

if(err == nil){

    NSLog(@"读取文件成功,%@",str);

} else {

    NSLog(@"%@",err);

}

其中，encoding:NSUTF8StringEncoding 中的 NSUTF8StringEncoding 是指定字符串的编码格式

error:&err 中将NSError中的指针地址传入，这样，如果解析不正确，那么这个err中将会包含错误信息。



11，可以通过指定磁盘上的URL来读取磁盘上某个文件的内容来创建字符串



NSURL *url=[NSURLURLWithString:@"file:///Users/mac/Desktop/test.txt"];

NSString *str2=[NSStringstringWithContentsOfURL:url encoding:NSUTF8StringEncodingerror:nil];

NSLog(@"%@",str2);



12，通过指定网络路径，获取网络上的内容来创建字符串。



NSURL *url3=[NSURLURLWithString:@"http://www.baidu.com"];

NSString *str3=[NSStringstringWithContentsOfURL:url3 encoding:NSUTF8StringEncodingerror:nil];

NSLog(@"%@",str3);