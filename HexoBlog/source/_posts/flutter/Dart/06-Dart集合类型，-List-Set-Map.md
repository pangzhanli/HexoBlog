---
title: '06-Dart集合类型， List, Set, Map'
toc: true
date: 2020-09-01 21:21:11
tags:
categories:
- flutter
- Dart语法
---


1, List 里面常用的属性和方法：

常用属性：
length:  			长度
reversed			反转
isEmpty			是否位空
isNotEmpty		是否不位空
常用方法：
add				添加
addAll			添加数组
indexOf			查找， 传入具体的值
remove			删除， 传入具体的值
removeAt			删除， 传入索引值
fillRange			修改
insert(index, value)  指定位置插入
insertAll(index, list)	指定位置插入List
toList()			其他类型转换成List
join()			List转换成字符串
split()			切割
forEach()			//循环，不带返回值
map()			//循环，带有返回值
where()			//循环， 返回符合条件的
any()			//循环，只要有一个满足条件，就返回true,  否则返回false
every()			//循环,   每一个都满足条件， 才返回true， 否则返回false


2, 
 //forEach方法：

  // List myList = ["桃子","西瓜","苹果"];
  // myList.forEach((value){
  //   print("$value");
  // });


//map方法：
  // List myList = [1,3,4];
  // var newList = myList.map((value){
  //   return value * 2;
  // });
  // print(newList);           //(2, 6, 8)        
  // print(newList.toList());  //[2, 6, 8]


// //where方法：
//   List myList = [1,3,4,5,6,7,8];
//   var newList = myList.where((value){
//     return value > 5;   //返回条件 > 5的
//   });

//   print(newList);   //(6, 7, 8)


// //any方法： 
//   List myList = [1,3,4,5,6,7,8];

//   //只要集合里面有一个满足条件，就返回true
//   var f = myList.any((value){
//     return value > 5;
//   });

//   print(f); //true


// // every方法：
//   //集合中每一个都要满足条件，返回true, 否则返回false
//   List myList = [1,3,4,5,6,7,8];

//   //
//   var f = myList.every((value){
//     return value > 5;
//   });
//   print(f);   //false


//Set的遍历
  // var s = new Set();
  // s.add("111");
  // s.add("222");

  // //只有一行，可以使用 => 
  // s.forEach((value)=>print(value));

  Map person = {
    "name":"张三",
    "age":20
  };

  person.forEach((key,value){
    print("$key:$value");
  });



## 参考资料
> - []()
> - []()
