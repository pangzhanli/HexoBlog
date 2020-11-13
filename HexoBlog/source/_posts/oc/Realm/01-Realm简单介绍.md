---
title: 01-Realm简单介绍
toc: true
date: 2020-10-15 20:50:13
tags: Realm
categories:
- OC
- Realm
---



# 一,  简介
realm是一个跨平台移动数据库引擎，支持ios, OSX(objective-c 和 swift) 以及 android, 核心数据引擎是由c++打造，并不是建立在SQLite之上的ORM, 是拥有独立的数据库存储引擎。

 - 性能： 比sqlite, coredata牛逼
 - 易用：相比于sqlite, coredata, 使用起来更加简单，更易入门。

# 二，使用教程：

https://realm.io/docs/objc/latest/

# 三，辅助工具
 
Realm Browser 或者 Xcode插件

# 四，安装方法有4种

### 1: 动态类库  Dynamic Framework

注意： 动态类库与ios7不兼容，要支持ios7的话，请查看静态框架

 - 1.下载最新的Realm发行版本，并解压；
 - 2.前往Xcode 工程的”General”设置项中，从ios/dynamic/、osx/、tvos/ 或者watchos/中将’Realm.framework’拖曳到”Embedded Binaries”选项中。确认Copy items if needed被选中后，点击Finish按钮；
 - 3.在单元测试 Target 的”Build Settings”中，在”Framework Search Paths”中添加Realm.framework的上级目录；
 - 4.如果希望使用 Swift 加载 Realm，请拖动Swift/RLMSupport.swift 文件到 Xcode 工程的文件导航栏中并选中Copy items if needed；
 - 5.如果在 iOS、watchOS 或者 tvOS 项目中使用 Realm，请在您应用目标的”Build Phases”中，创建一个新的”Run Script Phase”，并将
bash "${BUILT_PRODUCTS_DIR}/${FRAMEWORKS_FOLDER_PATH}/Realm.framework/strip-frameworks.sh"
这条脚本复制到文本框中。 因为要绕过APP商店提交的bug，这一步在打包通用设备的二进制发布版本时是必须的。

### 2:CocoaPods 

在项目的Podfile中，添加pod 'Realm'，在终端运行pod install。

### 3:Carthage

 - 1.在Carthage 中添加github "realm/realm-cocoa"，运行carthage update。为了修改用以构建项目的 Swift toolchain，通过--toolchain参数来指定合适的 toolchain。--no-use-	 binaries参数也是必需的，这可以避免 Carthage 将预构建的 Swift 3.0 二进制包下载下来。 例如：
carthage update --toolchain com.apple.dt.toolchain.Swift_2_3 --no-use-binaries
 - 2.从 Carthage/Build/目录下对应平台文件夹中，将 Realm.framework
拖曳到您 Xcode 工程”General”设置项的”Linked Frameworks and Libraries”选项卡中；
 - 3.iOS/tvOS/watchOS: 在您应用目标的“Build Phases”设置选项卡中，点击“+”按钮并选择“New Run Script Phase”。在新建的Run Script中，填写: /usr/local/bin/carthagecopy-frameworks 在“Input Files”内添加您想要使用的框架路径，例如: $(SRCROOT)/Carthage/Build/iOS/Realm.framework 因为要绕过APP商店提交的bug，这一步在打包通用设备的二进制发布版本时是必须的。

 - 4: Static Framework (iOS only)
 
	下载 Realm 的最新版本并解压，将 Realm.framework 从 ios/static/文件夹拖曳到您 Xcode 项目中的文件导航器当中。确保 Copy items if needed 选中然后单击 Finish；
	在 Xcode 文件导航器中选择您的项目，然后选择您的应用目标，进入到 Build Phases 选项卡中。在 Link Binary with Libraries 中单击 + 号然后添加libc++.dylib；

