---
title: flutter 动画
date: 2020-10-19 10:42:36
tags: flutter
---

## customPaint
自绘组件可以使用customPaint组件绘制

## 动画快速入门

动画核心是AnimationController

AnimationController 有四种状态：

1.  forward 开始动画
2.  reverse 反转动画
3.  complete 在结尾停止动画
4.  dismissed 在动画开始停止时

AnimationController 有多种动作：

1. forward
2. repeat
3. stop
4. dispose

套路是用AnimationController控制属性值,通常是在initState设置controller的动作。

1. 初始化AnimationController

```dart
initState() {
    c = AnimationController(vsync: this, durantion: Duration(milliseconds: 500))..addListen((){
        // 动画开始就会被监听到
        setState(){
            size = 100 + 100 * c.value;
        }
    })
    ..addStatusListener((statues) {
        // 监听动画的多个状态，并在不同的状态做不同的处理
        switch (status) {
            case AnimationStatus.completed:
            animationController.reverse();
            break;
            case AnimationStatus.dismissed:
            animationController.forward();
            break;
            default:
        }
    }); 
}

```
2. 设置对应的变化属性到对象上

```dart
Container(
    width: _size,
    height: _size, 变化属性
    color: animationColor.value,
),
```

3. 设置触发事件

```dart
MaterialButton(
    onPressed: () {
    animationController.forward();
    },
    child: Text('sizeAnimation'),
)
```

## Tween变化
flutter内置很多tween用于处理不同类型的值，比如颜色，border。

@init 这里会返回一系列BorderRadiusTween.value,是BorderRadius对象实例，把返回的值放到对应的BorderRadius盒子属性即可。

```dart
    animationBorder = BorderRadiusTween(
            begin: BorderRadius.all(Radius.circular(0)),
            end: BorderRadius.all(Radius.circular(50)))
        .animate(animationController);

```
@build

```dart
Row(
    mainAxisAlignment: MainAxisAlignment.center,
    children: <Widget>[
    Container(
        margin: EdgeInsets.only(top: 10),
        width: 100,
        height: 100,
        decoration: BoxDecoration(
            color: Colors.deepPurple,
            border: Border.all(width: 1, color: Colors.transparent),
            borderRadius: animationBorder.value),
    )
    ],
),
MaterialButton(
    onPressed: () {
    animationController.forward();
    },
    child: Text('borderRaduis'),
)
```

ColorTween

## border家族

    ShapeBorder
        |
    BoxBorder
      /   \
Border     BorderDirectional