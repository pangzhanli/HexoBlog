---
title: 14-Dart中自定义库，系统库，第三方库
toc: true
date: 2020-09-01 21:22:58
tags:
categories:
- flutter
- Dart语法
---

1，自定义库，将 自定义类Person单独抽出去，放到一个单独的文件中，然后通过import的方式引入，这个Person.dart就是自定义的库。
2，引入系统库

引入 math库
import 'dart:math';

//求最小数和最大数
print(min(10,20));
print(max(10,20));

引入io和convert库
import 'dart:io';
import 'dart:convert';


/**
 * async 是让方法变成异步
 * await 是等待异步方法执行完成
 */
getDataFromZhiHuAPI() async{
  //1. 创建HttpClient对象
  var httpClient = new HttpClient();
  //2. 创建Uri对象 http://news-at.zhihu.com/api/3/stories/latest
  var uri = new Uri.http("news-at.zhihu.com", "/api/3/stories/latest");
  //3. 发起请求，等待结束
  var request = await httpClient.getUrl(uri);
  //4. 关闭请求，等待响应
  var response = await request.close();
  //5. 解码相应的内容
  return response.transform(utf8.decoder).join();
}

调用方法：
var result = await getDataFromZhiHuAPI();
print(result);


3，导入第三方库
pub包管理系统
  1. 从下面网址找到要用的库
https://pub.dev/packages
https://pub.flutter-io.cn/packages
https://pub.dartlang.org/flutter

2. 创建一个pubspec.yaml 文件，内容如下：

name: thisAPubSettingFile
description : A new flutter module project
dependencies:
    	http: ^0.12.0+4
   	date_format: ^1.0.8
3. 配置 dependencies
4. 运行 pub get 获取远程库到本地
5. 看文档引入库使用。

使用：
import 'dart:convert' as convert;
import 'package:http/http.dart' as http;

void main(List<String> args) async {

  var url = 'http://news-at.zhihu.com/api/3/stories/latest';

  var response = await http.get(url);
  if (response.statusCode == 200) {
    var jsonResponse = convert.jsonDecode(response.body);
    print(jsonResponse);
  } else {
    print('Request failed with status: ${response.statusCode}.');
  }
}

4. Dart库冲突
多个文件中，有相同的类，那么引入的时候，怎么办呢？
使用 as 关键字指定, 
例如： Person1.dart文件和Person2.dart中都有 Person类

import 'lib/Person1.dart';
import 'lib/Person2.dart' as lib;

使用：
Person p1 = new Person("张三",20); //这里的Person使用的Person1.dart文件中的Person类

lib.Person p2 = new lib.Person("李四",30);  //这里的Person类就是Person2.dart文件的Person类

5，如果一个类库有很多方法，我们只需要其中的一个，或者多个，用不到的就不用引用，但是，它们都是在一个文件中，怎么办呢？

解决这种问题，有两种模式：
模式一： 只导入需要的部分，使用 show 关键字，例如：
import "package:lib1/lib1.dart" show foo;   //只引用foo

模式二：隐藏不需要的部分，使用hide关键字， 例如：
import "package:lib2/lib12.dart" hide  foo;  //隐藏foo, 其他的都引用



## 参考资料
> - []()
> - []()
