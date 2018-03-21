---
title: HashMap-源码分析
date: 2018-03-21 21:54:19
tags:
- 源码分析
---
>一个菜鸟的源码之路

![测试代码](https://upload-images.jianshu.io/upload_images/6555928-4919cad9bc183f21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
和之前分析的一样，我们来从初始化，加值，扩容这三个步骤来说。
 ## 1.new初始化

![](https://upload-images.jianshu.io/upload_images/6555928-f99963e2a9037d34.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/6555928-c7151ef5816c2d07.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在这里初始化了一个值，叫负载因子，具体的作用后面再说。
## 2.put加值
put函数就会直接调用`putVal()`
![](https://upload-images.jianshu.io/upload_images/6555928-fd866a4a33db3cf7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
再来看下`hash()`的实现,发现这个函数就是用来求传入值的hashcode值的异或运算结果。具体作用主要是，来将一个一个对象进行区域划分，减少查找难度
![](https://upload-images.jianshu.io/upload_images/6555928-d663d35e59a7f6fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
然后，来分析下`putVal()`函数。这部分比较长，我们一步一步来分析。
![](https://upload-images.jianshu.io/upload_images/6555928-dd19617d9ff6f2ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
首先会到`resize()`函数，我们来看下`resize()`函数。发现会返回一个16长度的Node数组
![](https://upload-images.jianshu.io/upload_images/6555928-fdea8e7fc7ef3b93.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

再来看`putVal()`函数。然后就会将保存了key，value的Node节点赋给tab[i]。
![](https://upload-images.jianshu.io/upload_images/6555928-753634c7ae964944.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3.扩容
之前说到，最初是初始化一个长度为16的数组，当长度超过时，会咋样呢。这时，我们就要回过头来看`resize()`函数
![](https://upload-images.jianshu.io/upload_images/6555928-2ce16eef4edf4a0b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
此时，我们知道了负载因子的作用。每当存储的键值对的长度大于负载因子和默认大小的乘积时，会自动扩容为原来的一倍
