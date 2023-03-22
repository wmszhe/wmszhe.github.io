---
title:       'Android生成jks时遇到的'
date:        '2019-11-01'
description: ''
author:      ''
image:       ''
tags:
    - Android
categories:
    - 
---

keytool -importkeystore -srckeystore /Users/zhe/Desktop/Test.jks -destkeystore /Users/zhe/Desktop/Test_sign.jks -deststoretype PKCS12

<!--more-->


### 生成jks

1. 通过AndroidStudio生成
2. 通过命令生成


#### 生成jks文件后，会有个Warning

> jks密钥库使用专用格式建议使用keytool my release key keystore my release key keystore pkcs12迁移到行业标准格式pkcs12

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/QQ20191101-104757@2x.png)

#### 解决方案：

```
keytool -importkeystore -srckeystore srckey -destkeystore targetkey -deststoretype pkcs12
```

==注意srckey和targetkey不能相同,否则会报如下错误==

```
keytool 错误: java.io.IOException: DerInputStream.getLength(): lengthTag=109, too big.
```

#### eg:

```
keytool -importkeystore -srckeystore /Users/zhe/Desktop/Test.jks -destkeystore /Users/zhe/Desktop/Test_sign.jks -deststoretype PKCS12
```