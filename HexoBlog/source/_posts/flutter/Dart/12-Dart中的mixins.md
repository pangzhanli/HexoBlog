---
title: 12-Dart中的mixins
toc: true
date: 2020-09-01 21:22:40
tags:
categories:
- flutter
- Dart语法
---

mixins的中文意思是混入，就是在类中混入其他功能。
在Dart中可以使用mixins实现类似多继承的功能

因为mixins使用的条件，虽则Dart版本一直在改变，这里讲 Dart2.x中使用mixins的条件：
1，作为mixins 的类只能继承自object, 不能继承其他类。
2，作为mixins的类不能有构造函数。
3，一个类可以mixins多个mixins类。
4，mixins绝不是继承，也不是接口，而是一种全新的特性。

例子：

class Person{
  String name;
  int age;
  Person(this.name,this.age);

  void printUserInfo(){
    print("${this.name} --- ${this.age}");
  }

  void run(){
    print("Person run");
  }
}

class A{
  void printA(){
    print("printA");
  }

  void run(){
    print("A - Run");
  }
}

class B{
  void printB(){
    print("printB");
  }

  void run(){
    print("B - Run");
  }
}

class C extends Person with B,A{
  C(String name, int age) : super(name, age);

  void printC(){
    print("printC");
  }
}


  // C c = new C();
  // c.printA();
  // c.printB();
  // c.printC();

  /** 打印结果:
printA
printB
printC
   */

  C c1 = new C("张三", 20);
  c1.run();
  c1.printUserInfo();

打印结果：

A - Run
张三 --- 20



## 参考资料
> - []()
> - []()
