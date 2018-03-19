---
title: HashSet-源码分析
date: 2018-03-19 22:57:03
tags:
- 源码分析
---
> 一个菜鸟的源码之路

![测试代码](https://upload-images.jianshu.io/upload_images/6555928-7d838492a9edaac5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 1.new初始化
看new函数，发现hashset底层实际是hashmap,初始化一个hashset，实际就是初始化了一个hashmap
![](https://upload-images.jianshu.io/upload_images/6555928-88eb62c4f67b37d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 2.add添加元素
添加一个元素实际就是在hashmap中插入一个值
![](https://upload-images.jianshu.io/upload_images/6555928-df0bb14c0354551c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
来看下`PRESENT`,每次插入的key就是你要保存的值，而value都是指向一个新建的对象，由于这个新建对象是`private static final`,所以PRESENT都是同一个。主要是利用hashmap的key唯一性来保证hashSet的唯一性
![](https://upload-images.jianshu.io/upload_images/6555928-9749f5e1e4e0b937.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3.size求大小
通过调用hashmap的接口来实现
![](https://upload-images.jianshu.io/upload_images/6555928-41f308ef6130b4d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



由此可见，hashSet原理就是hashMap。hashMap会在接下来讲解到。



