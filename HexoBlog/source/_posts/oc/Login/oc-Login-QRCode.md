---
title: IOS扫码登录
date: 2020-04-08 18:07:19
categories: 
- OC
- 登录
tags: 登录
---

很多的网站，或者桌面应用都用了手机扫码登录的功能，现在，我们了解一下，扫码登陆的大致过程：

1. 浏览器输入网站地址，展示登录二维码信息等。
2. 手机通过扫描二维码，确认登录。
3. 网页或者桌面应用检测到手机允许登录，生成用户信息登录成功。

小编从网上找了一张图片(懒得画)，大致流程图：
![](oc-Login-QRCode/ios_qrcode_login.jpeg)

小编个人感觉：

1. 第1步， 主要是产生一个key或者token, 甭管是前端自己产生，还是调用服务端接口产生的，必须得加上标识，这样，app端扫码之后，获取二维码的字符串之后，通过解析，知道这是一个要登录的二维码，进而跳转到扫码登录界面去了。要不然，app的扫码怎么知道这是一个要登录的二维码，而不是支付的二维码呢？
2. 第2步，上图是轮询，这个看心情，看技术等等（咋看都行），长连接也ok的，怎么高兴怎么来。
3. 

