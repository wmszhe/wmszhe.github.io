---
title:       'Android添加一个view到多个view中去'
date:        '2020-09-02'
description: ''
author:      ''
image:       ''
tags:
    - Android
    - Java
categories:
    - 
---

Java Class.forName

<!--more-->

### Android添加一个view到多个view中去

> 假如有一个view: View view = new View();
>
> 有多个FrameLayout: FrameA，FrameB
>
> 如果要将view添加到FrameA，FrameB，调用FrameA.addView(view)，再FrameB.addView(view)时，会提示view已经有一个父View了，不能添加成功。

此时，我们可以通过Class.forName，来实现这个功能

```
try {
    // 根据view加载view的class
    Class<?> clazz = Class.forName(view.getClass().getName());
    // 调用带Context的构造函数
    Constructor<?> constructor = clazz.getConstructor(Context.class);
    // 生成一个新的view对象
    View view = (View) constructor.newInstance(mContext);
    // 添加
    frame.addView(view);
} catch (Exception e) {
    e.printStackTrace();
}
```

### Class.forName说明

#### 一. 什么时候用Class.forName()

给你一个字符串变量，它代表一个类的包名和类名，你怎么实例化它？你第一想到的肯定是new，但是注意一点：
 A a = (A)Class.forName(“pacage.A”).newInstance();
 A a = new A();

 是一样的效果。

#### 二. 用法

> 如果被调用的类的构造函数为默认的构造函数，采用Class.newInstance() 
>
> 如果需要调用类的带参构造函数、私有构造函数， 就需要采用Constractor.newInstance()

1. 加载无参数的类

   ```
   try {
       Class<?> clazz = Class.forName("A");
       A a = (A) clazz.newInstance();
   } catch (Exception e) {
       e.printStackTrace();
   }
   ```

2. 加载有参数的类

   ```
   // 带context参数
   try {
       Class<?> clazz = Class.forName("A");
       Constructor<?> constructor = clazz.getConstructor(Context.class);
       A a = (A) constructor.newInstance(mContext);
   } catch (Exception e) {
       e.printStackTrace();
   }
   // 其他参数
   try {
       Class<?> clazz = Class.forName("A");
       Constructor<?> constructor = clazz.getConstructor(new Class[]{int.class, String.class});
       A a = (A) constructor.newInstance(new Object[]{5, "abc"});
   } catch (Exception e) {
       e.printStackTrace();
   }
   ```

### 参考

1. [https://blog.csdn.net/kaiwii/article/details/7405761]()
2. [https://www.cnblogs.com/xiaoenduke/p/10854657.html]()