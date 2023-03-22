---
title:       'FLutter编译桌面端app'
date:        '2019-06-18'
description: ''
author:      ''
cover:
    image: 'https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/flutter-bian-yi-zhuo-mian-duan-app.png'
tags:
    - Flutter
categories:
    - 
---

使用[flutter-desktop-embedding](https://github.com/google/flutter-desktop-embedding)编译适用于macos、windows、linux桌面端的app

<!--more--> 

#### 流程

1. 配置flutter环境，必须在master分支
    ```
    flutter channel master
    flutter upgrade
    ```
2. clone flutter-desktop-embedding
    ```
    git clone git@github.com:google/flutter-desktop-embedding.git
    ```
3. 复制flutter-desktop-embedding/example到自己的开发目录下,重命名为flutter_desktop
    
    > 目前不支持flutter create直接创建desktop项目，只能复制出example项目修改
4. 开启ENABLE_FLUTTER_DESKTOP
    - **一次性，每次打开项目都要执行** 
        ```
        命令行中 export ENABLE_FLUTTER_DESKTOP=true
        ```
    - **永久** 
        ```
        .zshrc中添加 export ENABLE_FLUTTER_DESKTOP=true
        ```
    - **如果使用的是vscode**
        ```
        打开设置(json)，添加
        "dart.env": {
            "ENABLE_FLUTTER_DESKTOP": true,
        }
        ```
5. 更新依赖
    ```
    flutter packages get
    ```
6. flutter run,即可看到demo项目		
		```
		flutter run
	    ```
		![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1560851493604.png)
7. 使用文本编辑器打开flutter_desktop项目，在lib目录下编写自己的代码
    ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1560850644118.png)
8. over!