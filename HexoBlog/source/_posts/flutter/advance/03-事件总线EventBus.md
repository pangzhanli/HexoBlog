---
title: 03-事件总线EventBus
toc: true
date: 2021-01-21 19:16:52
tags: 进阶
categories:
- flutter
- 进阶
---


在APP中，我们经常会需要一个广播机制，用以跨页面事件通知，比如一个需要登录的APP中，页面会关注用户登录或注销事件，来进行一些状态更新。这时候，一个事件总线便会非常有用，事件总线通常实现了订阅者模式，订阅者模式包含发布者和订阅者两种角色，可以通过事件总线来触发事件和监听事件。

# 一，源码分析

```
class EventBus {
  StreamController _streamController;
  StreamController get streamController => _streamController;

  EventBus({bool sync = false})
      : _streamController = StreamController.broadcast(sync: sync);

  EventBus.customController(StreamController controller)
      : _streamController = controller;

  Stream<T> on<T>() {
    if (T == dynamic) {
      return streamController.stream;
    } else {
      return streamController.stream.where((event) => event is T).cast<T>();
    }
  }

  void fire(event) {
    streamController.add(event);
  }

  void destroy() {
    _streamController.close();
  }
}
```

简单分析源码可得，EventBus 核心主要是通过 Stream 来进行事件分发的，
 
 - 其中初始化时会创建一个 StreamController.broadcast(sync: sync) 广播流；
 - fire() 广播发送方法主要是向 StreamController 中添加事件；
 - on() 为广播监听，都是对 Stream 流操作；


# 二，EventBus封装

### 1, EventBus管理类封装


```
import 'dart:async';

import 'package:event_bus/event_bus.dart';
import 'package:flutter/material.dart';
import 'package:gm_utils/src/event_bus/event_bus_observer_widget.dart';

///EventBus管理类
class GMEventBusManager {
  EventBus _eventBus;

  //内部静态实例
  static GMEventBusManager _instance;
  GMEventBusManager._internal() {
    //初始化
  }
  //内部静态方法
  static GMEventBusManager _getInstance() {
    if (_instance == null) {
      _instance = new GMEventBusManager._internal();
      _instance._eventBus = EventBus(); // 创建事件总线
    }
    return _instance;
  }

  //工厂模式
  factory GMEventBusManager() => _getInstance();
  //实例方法
  static GMEventBusManager get instance => _getInstance();

  /// 订阅者
  static Map<Type, List<StreamSubscription>> subscriptions = {};

  /// 添加监听事件
  /// [T] 事件泛型 必须要传
  /// [onData] 接收到事件
  static StreamSubscription onObserverEvent<T extends Object>(
      void onData(T event),
      {Function onError,
      void onDone(),
      bool cancelOnError}) {
    StreamSubscription subscription = GMEventBusManager.instance?._eventBus
        ?.on<T>()
        ?.listen(onData,
            onError: onError, onDone: onDone, cancelOnError: cancelOnError);

    if (subscriptions == null) subscriptions = {};
    List<StreamSubscription> subs = subscriptions[T.runtimeType] ?? [];
    subs.add(subscription);
    subscriptions[T.runtimeType] = subs;

    return subscription;
  }

  /// 监听组件
  /// [T] 事件泛型 必须要传
  /// [observer] 要监听的组件回调
  static Widget onObserverWidght<T extends Object>(
    Widget Function(BuildContext context, dynamic event) observer,
  ) {
    return GMEventBusObserverWidget<T>(
      observer: observer,
    );
  }

  /// 移除监听者
  /// [T] 事件泛型 必须要传
  /// [subscription] 指定
  static void off<T extends Object>({StreamSubscription subscription}) {
    if (subscriptions == null) subscriptions = {};
    if (subscription != null) {
      // 移除传入的
      List<StreamSubscription> subs = subscriptions[T.runtimeType] ?? [];
      subs.remove(subscription);
      subscriptions[T.runtimeType] = subs;
      subscription.cancel();
    } else {
      List<StreamSubscription> subs = subscriptions[T.runtimeType] ?? [];
      for (StreamSubscription tmpSubscription in subs) {
        tmpSubscription.cancel();
      }
      // 移除全部
      subscriptions[T.runtimeType] = null;
    }
  }

  /// 发送事件
  static void fire(event) {
    debugPrint("fire start:  $event");
    debugPrint(
        "fire:  ${GMEventBusManager.instance},  ${GMEventBusManager.instance?._eventBus},");
    GMEventBusManager.instance?._eventBus?.fire(event);
    debugPrint("fire end :  $event");
  }
}

```

### 2, EventBus观察者组件

```
import 'dart:async';

import 'package:flutter/material.dart';

import 'event_bus_manager.dart';

///EventBus观察者组件
class GMEventBusObserverWidget<T extends Object> extends StatefulWidget {
  ///观察者
  Widget Function(BuildContext context, dynamic event) observer;

  GMEventBusObserverWidget({Key key, this.observer}) : super(key: key);

  @override
  _GMEventBusObserverWidgetState<T> createState() =>
      _GMEventBusObserverWidgetState<T>();
}

class _GMEventBusObserverWidgetState<T extends Object>
    extends State<GMEventBusObserverWidget> {
  StreamSubscription<T> subscription;
  T tmpEvent;
  @override
  void initState() {
    this.subscription = GMEventBusManager.onObserverEvent<T>((event) {
      if (mounted) {
        setState(() {
          tmpEvent = event;
        });
      }
    });

    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return this.widget.observer(context, tmpEvent);
  }

  @override
  void dispose() {
    GMEventBusManager.off<T>(subscription: this.subscription);
    debugPrint("_GMEventBusObserverWidgetState dispose");
    super.dispose();
  }
}
```


### 3，使用示例：

```
//发送事件
RaisedButton(
  child: Text("test5"),
  onPressed: () {
    int count = Random().nextInt(1000);
    GMTestPage5Event test5Event = GMTestPage5Event();
    test5Event.title = "$count";
    GMEventBusManager.fire(test5Event);
  },
),

//1. 通过返回组件的形式进行监听
...
GMEventBusManager.onObserverWidght<GMTestPage5Event>(
    (BuildContext ctx, dynamic event) {
  String title = "";
  if (event != null) {
    title = event.title;
  }
  return Container(
    child: Text(title),
  );
}),
...

//2. 统一监听
...
@override
void initState() {
	GMEventBusManager.onObserverEvent<GMTestPage5Event>((event) {
	  debugPrint("_GMExampleAnimationTestPage5State  initState : $event,   ${event.title}");
	});

	super.initState();
}

//必须要重写
@override
void dispose() {
	super.dispose();
	
	//移除事件监听
	GMEventBusManager.off<GMTestPage5Event>();
	
	debugPrint("_GMExampleAnimationTestPage5State dispose");
}

```


> 注意：上边的监听使用了2种形式，一种是返回组件的形式进行监听，第二种是在initState方法中，统一进行监听。需要在dispose方法中，进行时间监听的移除。


# 三，混入监听

### 1, 混入监听分析
通过测试发现，这种初始化(initState)监听, 以及销毁时移除(dispose), 必须重写，能不能有一种更好的办法，我们直接使用，其他的啥也不用关心。基于此，我们使用混入的形式进行了封装。

混入源码：

```
import 'dart:async';

import 'package:flutter/material.dart';
import 'package:gm_utils/gm_utils.dart';

mixin GMEventBusObserverMixin<T extends StatefulWidget> on State<T> {
  /// 订阅者
  List<StreamSubscription> eventBusSubscriptions = [];

  @protected
  void addEventBusListeners();

  @override
  void initState() {
    super.initState();
    debugPrint("GMEventBusObserverMixin initState");
    this.addEventBusListeners();
  }

  ///添加监听事件
  void addEventBusListener<T>(void onData(T event)) {
    this.eventBusSubscriptions.add(GMEventBusManager.onObserverEvent(onData));
  }

  ///发送事件
  void eventBusFire<T>(T event) {
    GMEventBusManager.fire(event);
  }

  @override
  void dispose() {
    super.dispose();

    debugPrint("GMEventBusObserverMixin dispose");
    if (this.eventBusSubscriptions != null) {
      for (StreamSubscription subscription in this.eventBusSubscriptions) {
        subscription.cancel();
      }
      this.eventBusSubscriptions.clear();
    }
  }
}
```

### 2, 使用

```
class GMExampleAnimationTestPage6 extends StatefulWidget {
  GMExampleAnimationTestPage6({Key key}) : super(key: key);

  @override
  _GMExampleAnimationTestPage6State createState() =>
      _GMExampleAnimationTestPage6State();
}

class _GMExampleAnimationTestPage6State
    extends State<GMExampleAnimationTestPage6> with GMEventBusObserverMixin {
  
  //添加事件监听
  @override
  void addEventBusListeners() {
    this.addEventBusListener<GMExampleAnimationTestEvent>(
        (GMExampleAnimationTestEvent event) {
      debugPrint("addEventBusListener : $event,   ${event.title}");
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: example_common_appBar(context, "test5"),
      body: Container(
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            RaisedButton(
              child: Text("test5"),
              onPressed: () {
                //事件发送
                int count = Random().nextInt(1000);
                GMExampleAnimationTestEvent event =
                    GMExampleAnimationTestEvent();
                event.title = "$count";
                this.eventBusFire<GMExampleAnimationTestEvent>(event);
              },
            ),
          ],
        ),
      ),
    );
  }
}
```
