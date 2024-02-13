---
title:       'AS3.0以后，debug包INSTALL_FAILED_TEST_ONLY问题'
date:        '2020-06-30'
description: ''
author:      'wmszhe'
image:       ''
tags:
   - Android
categories:
    - 
---

> Android Studio 3.0以后，通过IDE直接run出来的安装包，有些手机无法直接安装，会提示`Failed to install app-debug.apk: Failure [INSTALL_FAILED_TEST_ONLY: installPackage]`

<!--more-->

### 问题

Android Studio 3.0以后，通过IDE直接run出来的安装包，无法直接安装，也无法通过`adb install xx.apk`的方式来安装。会提示`Failed to install app-debug.apk: Failure [INSTALL_FAILED_TEST_ONLY: installPackage]`

大多数手机上，我们可以通过`adb install -t xx.apk`的方式来安装，但是某些`OPPO`手机上，还是无法安装。

### 原因

IDE 直接 Run 出来的 APK ，会在 AndroidManifest.xml 文件中，增加 `android:testOnly="true"` 属性，正是因为这个属性，阻止了我们使用正常方式安装 APK。

### 解决方法

##### 1. 方法一（修改打包方式）

1. 当我们需要debug包的时候，不使用IDE直接run跑出的apk，而是通过IDE中gradle中，app-build-build命令来生成
2. 通过IDE菜单工具栏-Build-Build Bundle(s)/APK(s)来生成apk

##### 2. 方法二（会造成其他问题，不推荐）

在项目gradle.properties(或者gradle全局配置目录 ~/.gradle/)文件中添加`android.injected.testOnly=false`

<mark>此方法，会造成IDE run apk的时候，app无法直接打开启动页面，直接返回到桌面</mark>

### 不同方式打包，反编译结果

1. IDE直接run出来的apk

   <mark>带有`android:testOnly="true"`</mark>

   ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/mAUnTd.png)

   ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/VvYXPZ.png)

2. gradle-app-build-build编译出的apk

   <mark>不带`android:testOnly="true"`</mark>

   ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/rXpCsw.png)

   ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/drCtsQ.png)

3. IDE菜单工具栏-Build-Build Bundle(s)/APK(s)编译出的apk

   <mark>不带`android:testOnly="true"`</mark>

   ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/gjFOvf.png)

   ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/AFMm6U.png)


