---
title:       'Flutter遇到的问题'
date:        '2019-08-22'
description: ''
author:      'wmszhe'
image:       ''
tags:
    - Android
    - Flutter
categories:
    - 
---

Flutter开发过程中遇到的一些问题。

<!--more-->

### 1. Android设置Splash时图片拉伸解决方法

**设置splash：**

res/drawable/launch_backgroud.xml中，item-bitmap设置splash图片

```
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@android:color/white" />
    <item>
        <bitmap
            android:gravity="center|bottom"
            android:src="@mipmap/tk_splash" />
    </item>
</layer-list>
```

**图片拉伸解决方法**

==**图片要放在mipmap中，不能放在drawable中**==

mipmap分多个分辨率的文件夹。==如果只使用一张图片的话==，放在mipmap-mdpi下，图片会偏大，放在mipmap-xxxhdpi文件夹下，图片会偏小。经测试，放在mipmap-xhdpi文件夹下合适。

==**原因参考 [Android drawable微技巧，你所不知道的drawable的那些细节](https://blog.csdn.net/guolin_blog/article/details/50727753)**==

### 2. 多语言支持iOS无效，只显示英文

参考[Appendix: Updating the iOS app bundle](https://flutter.dev/docs/development/accessibility-and-localization/internationalization#appendix-updating-the-ios-app-bundle)



