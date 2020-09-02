---
title: 04-Dart运算符
toc: true
date: 2020-09-01 21:20:13
tags:
categories:
- flutter
- Dart语法
---

注： Dart 运算符有： 算数运算符， 关系运算符， 逻辑运算符， 赋值运算符， 
另外，这里还有 条件表达式， 类型判断。

1，算数运算符：  + - *  / (加减乘除),   ~/ （取整），  %（取余）
这里的 ~/ 取整运算符，  例如：  14~/10 = 2;

2, 关系运算符：  == ,  !=,   >,   <,   >=,   <=
3, 逻辑运算符:   !（取反）    &&    ||
4, 赋值运算符:
基础赋值运算符，   = ,      ??=
复合赋值运算符：  +=，  -=，  *=，  /=,   %=,    ~/=(取整等)
这里讲一下  ??= 这个运算符

var a = "111";
a??="222";

它的意思是：  如果a 为空，那么就会将222赋值给a。

5，条件表达式   
if else,    switch case， 跟其他语言一样，不再讲解。

三目运算符:
bool flat = true;
String str = flag ? "我是true":"我是false";
print(str);

?? 运算符:(如果为空，就直接赋值)
  var a;
  var b = a ?? 10;
  print(b);   // b=10, 已经被赋值

  var c = 20;
  var d = c ?? 30;  
  print(d);   //d=20, 因为c不等于空，有值

6, 类型转换，Number 与 String 之间的转换
Number类型转换成String类型：  toString()
String类型转换成Number类型：  int.parse() , double,parse()

其他类型转换成 boolean类型：
isEmpty 判断是否为空;
  var str;
  if(str == null){
    print("str is null");
  }else if(str.isEmpty){
    print("str 是 空");
  }else{
    print("str 非 空");
  }


  //NaN 类型
  var myNum = 0/0;
  print(myNum);

  if(myNum.isNaN){
    print("是 NaN 类型");
  }


## 参考资料
> - []()
> - []()
