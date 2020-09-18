---
title: 09-StatefulWidget生命周期
toc: true
date: 2020-09-02 20:38:22
tags:
categories:
- flutter
- flutter框架一
---


# 一： StatelessWidget 生命周期

1, 构造方法

2，build方法

# 二： StatefulWidget 生命周期

1，statefulWidget  类 的构造方法

2，statefulWidget  类  的createState方法

3，state  类的 构造方法

4，state  类的 initState方法

5，state  类的 build方法

6，state  类的dispose 方法

还有  didUpdateWidget 方法

涉及代码：

```
class HYContentBody extends StatefulWidget {
  HYContentBody(){
    print("1. HYContentBody --- 构造方法");
  }
  @override
  _HYContentBodyState createState(){
    print("2. HYContentBody --- createState 方法");
    return _HYContentBodyState();
  }
}

class _HYContentBodyState extends State<HYContentBody> {
  _HYContentBodyState(){
    print("3._HYContentBodyState --- 构造方法");
  }

  @override
  void didUpdateWidget(HYContentBody oldWidget) {
    super.didUpdateWidget(oldWidget);

    print("_HYContentBodyState --- didUpdateWidget 方法");
  }

  @override
  void initState() {
    super.initState();
    print("4._HYContentBodyState --- initState 方法");
  }
  @override
  Widget build(BuildContext context) {
    print("5._HYContentBodyState --- build 方法");
    return Text("test001");
  }

  @override
  void dispose() {
    super.dispose();

    print("6._HYContentBodyState --- dispose 方法");
  }
}
```



## 参考资料
> - []()
> - []()
