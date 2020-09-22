---
title: 'Hexo简单介绍'
date: 2020-04-02 16:52:27
categories: Hexo
tags:
---

## 一、hexo简介

#### 1, hexo是什么
> hexo(中文官方网站)是一个快速, 简洁且高效的博客框架. 让上百个页面在几秒内瞬间完成渲染. hexo支持Github Flavored Markdown的所有功能, 甚至可以整合Octopress的大多数插件. 并自己也拥有强大的插件系统.

#### 2, 安装

``` 
Hexo是基于node.js的, 所以我们在安装它之前需要用到npm安装工具, 这个工具是 node.js 安装包的工具, 所以, 我们先要安装 node.js.

可以使用 node -v 命令查询当前系统是否安装过nodejs
``` 

使用apt-get安装 nodejs.

``` 
$ sudo apt-get install -y nodejs
``` 

#### 3, 安装npm

``` 
可以使用 npm -v 命令查询当前系统是否安装过npm
``` 

安装npm 命令

``` 
$ sudo apt-get install npm
``` 

#### 4, 安装hexo

现在我们使用npm安装hexo.

``` 
$ sudo npm install hexo-cli -g
``` 

## 二、创建Blog

现在我们已经完成hexo的安装, 那么现在我们来创建一个Blog.

#### 1, 创建一个叫blog网站

``` 
$ hexo init blog
``` 

> 注: 如果不写blog, 就会在当前目录进行初始化. 如果后面跟了名子就会创建目录并在目录进行初始化操作, 以这个名子为目录名.


#### 2, 我们进入创建的blog目录里. 并运行该服务.

``` 
$ cd blog
$ npm install
$ hexo server
``` 

#### 3, 打开浏览器, 在地址栏输入http://localhost:4000/可以看到我们刚刚创建的blog首页.

#### 4, 修改blog目录下的_config.yml配置文件将网站自部署到Github上.

``` 
deploy:
  type: 'git'
  repository: https://github.com/pangzhanli/pangzhanli.github.io.git
  branch: master
``` 

>注意在type前面需要增加两个空格, 在type的冒号后面需要增加一个空格. 请保持代码风格一致. 否则会出现错误或是不正确的问题.

#### 5, 安装部署使用到的git插件.

在这里我们使用的是git源码管理工具, 所以, 我需要安装git包进行部署, 安装这个插件才能使用git进行自动部署

``` 
$ npm install hexo-deployer-git --save
``` 

#### 6, 进行生成网站
当我们部署网站前, 需要先生成静态网站. 它会自动在目录下创建public的目录, 并将新生成的网页存放在这个目录里.

``` 
$ cd blog
$ hexo g
``` 

#### 7, 进行自动部署网站, 注意部署前需要重新生成网站, 每一次修改后都需要重新生成网站并进行部署, 生成网站前第6步.
``` 
$ hexo d
``` 

如果在部署出现错误信息如果下: 请参考第5步, 需要安装git插件

``` 
ERROR Deployer not found: git
``` 


## 三、hexo常用命令

#### 1, 安装，升级，初始化

``` 
npm install hexo -g #安装  
npm update hexo -g #升级  
hexo init #初始化
``` 

#### 2, 简写：

``` 
hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo p == hexo publish
hexo g == hexo generate#生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy#部署
``` 

#### 3, 服务器：

``` 
hexo server #Hexo 会监视文件变动并自动更新，您无须重启服务器。
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP

hexo clean #清除缓存 网页正常情况下可以忽略此条命令
hexo g #生成静态网页
hexo d #开始部署
``` 

#### 4, 监视文件变动：

``` 
hexo generate #使用 Hexo 生成静态文件快速而且简单
hexo generate --watch #监视文件变动
``` 

完成后部署：

- 两个命令的作用是相同的
- hexo generate --deploy
- hexo deploy --generate

``` 
hexo deploy -g
hexo server -g
``` 

#### 5, 草稿

``` 
hexo publish [layout] <title>
``` 

#### 6, 模版

``` 
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub

hexo new [layout] <title>
hexo new photo "My Gallery"
hexo new "Hello World" --lang tw
``` 

| 变量 | 描述 |
| --- | --- | 
| layout | 布局 |
| title | 标题 |
| date | 文件建立日期 |

``` 
title: 使用Hexo搭建个人博客
layout: post
date: 2014-03-03 19:07:43
comments: true
categories: Blog
tags: [Hexo]
keywords: Hexo, Blog
description: 生命在于折腾，又把博客折腾到Hexo了。给Hexo点赞。
``` 
