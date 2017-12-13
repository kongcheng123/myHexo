---
title: Java == 和 equals
date: 2017-10-10 10:05:55
tags:
- java
categories:
- java
---
> 在java中，==和equals的使用有两种情况：字符串变量，和非字符串变量

- 对于字符串对象:
   1."=="是用来比较字符串本身的值，即两个字符串的内存首地址
   2."equals"是比较两个字符串的内容是否相同

![代码demo](http://upload-images.jianshu.io/upload_images/6555928-908353fb51f93375.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![结果](http://upload-images.jianshu.io/upload_images/6555928-dc0dca395bd2b7b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 对于非字符串对象
 1."=="和"equals"都是用来比较两个对象的地址的

![代码demo](http://upload-images.jianshu.io/upload_images/6555928-bb0eea3e44f9772b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![结果](http://upload-images.jianshu.io/upload_images/6555928-2e0498924d8af60e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
