---
title:       'FlutterUI相关'
date:        '2019-06-19'
description: ''
author:      ''
image:       'https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/flutterui-xiang-guan.png'
tags:
    - Flutter
categories:
    - 
---

获取屏幕尺寸，widget尺寸和位置

<!--more--> 

### 屏幕尺寸通过window相关方法获取

##### 屏幕尺寸（物理像素 px）
```
window.physicalSize -> Size(960.0, 720.0)
```
##### 屏幕密度
```
window.devicePixelRatio -> 2.0
```

### 屏幕尺寸通过MediaQuery相关方法获取

> MediaQuery最终还是调用的window方法

##### 屏幕尺寸（逻辑像素 dp）

> MediaQuery.of(context).size获取的是逻辑像素，物理像素/屏幕密度

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1560934244332.png)

```
MediaQuery.of(context).size -> Size(480.0, 360.0)
```

##### 屏幕密度
```
MediaQuery.of(context).devicePixelRatio -> 2.0
```

##### 横竖屏

> 横竖屏是根据宽高判断的

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1560934253781.png)

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1560934262800.png)

```
MediaQuery.of(context).orientation -> Orientation.landscape
```

### Widget大小和位置

#### 可以通过GlobalKey获取

> 参考：[Flutter : Widget Size and Position](https://medium.com/@diegoveloper/flutter-widget-size-and-position-b0a9ffed9407)

> 需要对每个widget创建一个GlobalKey

```
GlobalKey _keyRed = GlobalKey();
```

```
key: _keyRed,
```

```
RenderBox findRenderObject = _keyRed.currentContext.findRenderObject();
var offset = findRenderObject.localToGlobal(Offset.zero);
print("---icon offset : $offset");

var size = _keyRed.currentContext.size;
print("---icon size : $size");
```

#### 从context对象中获取


##### 自定义Widget时，可以从build方法中的context中获取

```
class CustomIcon extends Icon {
  CustomIcon(IconData icon) : super(icon);

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      child: Icon(icon),
      onTap: () {
        RenderBox findRenderObject = context.findRenderObject();
        var offset = findRenderObject.localToGlobal(Offset.zero);
        print("icon offset : $offset");

        var size = context.size;
        print("icon size : $size");
      },
    );
  }
}
```

##### 直接使用系统widget时，使用LayoutBuilder，LayoutBuilder提供了build方法中含有context对象

```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Row(
        children: <Widget>[
          LayoutBuilder(
            builder: (context, constraints) {
              return GestureDetector(
                child: MyIcon(Icons.dashboard),
                onTap: (){
                  RenderBox findRenderObject = context.findRenderObject();
                  var offset = findRenderObject.localToGlobal(Offset.zero);
                  print("---icon offset : $offset");

                  var size = context.size;
                  print("---icon size : $size");
                },
              );
            },
          ),
          MyIcon(Icons.ac_unit),
        ],
      ),
    );
  }
}
```

#### 在widget build完成之后，执行操作

> 在return一个widget之前，context为null，如果想要在build之后，立即获取一些属性，可以使用WidgetsBinding.instance.addPostFrameCallback((_) => afterBuild(context));

```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Row(
        children: <Widget>[
          LayoutBuilder(
            builder: (context, constraints) {
              WidgetsBinding.instance.addPostFrameCallback((_) => afterBuild(context));
              return Container(
                child: MyIcon(Icons.dashboard),
              );
            },
          ),
        ],
      ),
    );
  }

  afterBuild(BuildContext context) {
    RenderBox findRenderObject = context.findRenderObject();
    var offset = findRenderObject.localToGlobal(Offset.zero);
    print("---icon offset : $offset");

    var size = context.size;
    print("---icon size : $size");
  }
}
```

### 软键盘相关

#### 显示隐藏软键盘
1. 通过焦点方式

```
// 隐藏
FocusScope.of(context).requestFocus(FocusNode())
// 显示
FocusScope.of(context).autofocus(_focusNode)
```

2. 通过channel方式

```
// 显示
SystemChannels.textInput.invokeMethod('TextInput.show');
// 隐藏
SystemChannels.textInput.invokeMethod('TextInput.hide');
```
