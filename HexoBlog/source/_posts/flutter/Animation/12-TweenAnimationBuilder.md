---
title: 12-TweenAnimationBuilder
toc: true
date: 2020-10-29 14:42:23
tags: 动画
categories:
- flutter
- 动画组件
---

开发App中有时需要一个简单的动画，可以通过AnimationController实现，但比较麻烦，有没有一个内置的隐式动画组件来解决这个问题？TweenAnimationBuilder可以满足你对所有自定义动画的需求，而不用关系AnimationController。

效果：

![](12-TweenAnimationBuilder/12-TweenAnimationBuilder.gif)

代码:

```

class GMExampleTweenAnimationBuilderTest extends StatefulWidget {
  GMExampleTweenAnimationBuilderTest({Key key}) : super(key: key);

  @override
  _GMExampleTweenAnimationBuilderTestState createState() =>
      _GMExampleTweenAnimationBuilderTestState();
}

class _GMExampleTweenAnimationBuilderTestState
    extends State<GMExampleTweenAnimationBuilderTest> {
  double _value = 200;

  @override
  Widget build(BuildContext context) {
    return Center(
      child: TweenAnimationBuilder<double>(
        tween: Tween<double>(begin: 100.0, end: _value),
        duration: Duration(seconds: 1),
        // curve: Curves.bounceIn,
        curve: Curves.easeIn,
        builder: (context, value, child) {
          return Container(
            height: value,
            width: value,
            child: child,
          );
        },
        onEnd: () {
          setState(() {
            _value = _value == 200 ? 250 : 200;
          });
        },
        child: Image.network(
          "https://gfs5.gomein.net.cn/T1QMW7BCZT1RCvBVdK",
          fit: BoxFit.fill,
        ),
      ),
    );
  }
}

```