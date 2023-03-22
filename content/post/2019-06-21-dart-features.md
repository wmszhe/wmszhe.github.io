---
title:       'Dart一些特殊的特性'
date:        '2019-06-21'
description: ''
author:      ''
image:       ''
tags:
    - Flutter
    - Dart
categories:
    - 
---

Dart一些特殊的特性，比较容易忘记和混淆的

<!--more-->

### 参数加{}

> 在调用函数传递参数时，指定参数名

```
void sayHello({String name, String msg}){
    
}
sayHello(name: "abc", msg: "hello");
```

### 可选参数

> 可选的参数，在调用时可以不传

> 通过位置来确定实参和形参的对应关系的

> 参考： https://blog.csdn.net/xlh1191860939/article/details/87895616

```
String say(String from, String msg, [String device, String time]) {
 
    var result = "$from says $msg";
 
    if (device != null) {
      result = "$result with a $device";
    }
 
    if (time != null) {
      result = "$result at $time";
    }
 
    return result;
}
 
void main(){
    print(say("david", "hello", "mobile", "2019.2.29.20:08:08"));
    // david says hello with a mobile at 2019.2.29.20:08:08
    print(say("david", "hello", "2019.2.29.20:08:08", "mobile"));
    // david says hello with a 2019.2.29.20:08:08 at mobile
    print(say("david", "hello"));
    // david says hello
}
```

### ??=

> 仅在变量为null时赋值，使用??=运算符

```
// 如果b为空，则将值分配给b；否则，b保持不变
b ??= value;
```

### ?.

> eg : foo?.bar

> foo可以为空,foo为空时返回空，否则返回bar

```
foo?.bar

====等同于====

if(foo != null) {
    return bar;
} else {
    return null;
}
```

### / 和 ~/

> / 除

> ~/ 返回一个整数值的除法

```
assert(5 / 2 == 2.5); // 结果是double类型
assert(5 ~/ 2 == 2); // 结果是一个整数
```

### print

> 打印重复内容，可以使用*

> 如果要打印d.e，外层添加{}

```
print("abc");
print("abc $d");
print("abc ${d.e}");
print("abc" * 10); // 打印10次abc
```