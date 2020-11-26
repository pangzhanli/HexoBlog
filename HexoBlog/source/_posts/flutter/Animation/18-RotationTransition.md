---
title: 18-RotationTransition
toc: true
date: 2020-10-29 14:43:18
tags: 动画
categories:
- flutter
- 动画组件
---



效果：

![](18-RotationTransition/18-RotationTransition.gif)

代码:

```
class GMExampleRotationTransitionTest extends StatefulWidget {
  GMExampleRotationTransitionTest({Key key}) : super(key: key);

  @override
  _GMExampleRotationTransitionTestState createState() =>
      _GMExampleRotationTransitionTestState();
}

class _GMExampleRotationTransitionTestState
    extends State<GMExampleRotationTransitionTest>
    with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  Animation _animation;

  @override
  void initState() {
    _animationController =
        AnimationController(duration: Duration(seconds: 2), vsync: this);

    _animation = Tween(begin: 0.0, end: 0.5).animate(_animationController);

    //开始动画
    _animationController.forward();

    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return RotationTransition(
      turns: _animation,
      child: Container(
        height: 200,
        width: 200,
        color: Colors.red,
        alignment: Alignment.center,
        child: Text("test"),
      ),
    );
  }

  @override
  void dispose() {
    _animationController.dispose();

    super.dispose();
  }
}

```