---
title:       'Android性能优化'
date:        '2019-06-24'
description: ''
author:      'wmszhe'
image:       ''
tags:
    - 性能优化
    - Android
categories:
    - 
---

Android性能优化，一些性能优化方式。  

<!--more-->

##  删除多余依赖项

1. 查找多余依赖

    > 菜单栏 -> Analyze -> Run Inspection Name -> 输入unused library -> 回车 -> 查看分析结果
    
    ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1561599539057.png)
    
2. 查看module依赖
    
    > 使用gradle，依次确认各个module实际依赖情况

    ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1561599225931.png)
    
    ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1561368142795.png)
    
3. 排除多余依赖

    > 根据InspectionResult结果和dependencies结果，排除多余依赖项
    
    ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1561368152549.png)
    
    ![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1561599326748.png)
    

## 删除多余的资源文件

> 菜单栏 -> Analyze -> Run Inspection Name -> 输入unused Resources -> 回车 -> 查看分析结果 -> 删除

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/1561629719716.png)
