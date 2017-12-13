---
title: JVM之类文件结构 一
date: 2017-10-15 12:39:06
tags:
- jvm
---
>   计算机只认识0和1，所以我们写的程序需要经编译器翻译成由0和1构成的二进制格式才能由计算机执行。

## 1.概述
  java文件会被编译为class文件，而class文件是一组以8位字节为基础单位的二进制流。
  在Class文件结构中，有两种数据类型：无符号数和表。无符号数主要有以下四种类型：

| 类型        | 字节数    |
    | --------   | --  |
    | u1        | 1| 
    | u2        | 2      |
    | u4        | 4      | 
    | u8      | 8     |

  表就是由多个无符号数，以及其他的表组成的复杂的数据类型。
## 2.魔数
  每个Class文件的头4个字节称为魔数，用来确定这个文件是不是class文件。这四个字节的值为0xCAFEBABE（咖啡宝贝）。

![魔数](http://upload-images.jianshu.io/upload_images/6555928-fa76ff8c2978c991.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 3.主版本和次版本
  在魔数后面的两个字节是次版本号，为0x0000（为第五个和第六个字节），之后的为主版本号，为0x0032（为第七个和第八个字节）。

![主版本和次版本号](http://upload-images.jianshu.io/upload_images/6555928-441876876e4e720a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
注：高版本的JDK能向下兼容低版本的Class文件，但不能运行更高版本的Class文件
## 4.常量池
  紧接着主次版本号之后的是常量池。首先，是常量池容量计数值，是u2类型的数据。如图所示，为0x0024，及十进制的36，代表了有35个常量（1~35，0不算）。
![常量池容量计数值](http://upload-images.jianshu.io/upload_images/6555928-d774654363f55d45.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
常量池的第一项常量，0x0A代表了这个常量的数据类型，即10对应了CONSTANT_Methodref_info。

![常量池的项目类型](http://upload-images.jianshu.io/upload_images/6555928-c33864c64f046140.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在下方的表中找出CONSTANT_Methodref_info对应的结构，发现，该常量由u1，u2，u2个字节组成。
![](http://upload-images.jianshu.io/upload_images/6555928-c6a55deb9b8cc00f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![14项常量项的结构](http://upload-images.jianshu.io/upload_images/6555928-cc531c3a5904a815.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
