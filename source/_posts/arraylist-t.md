---
title: ArrayList-源码分析
date: 2018-03-19 22:11:42
tags:
- 源码分析
---
> 一个菜鸟的源码之路

![测试代码](https://upload-images.jianshu.io/upload_images/6555928-ecc0fa1d4b6dbcc6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 1.new初始化
1.当new一个ArrayList对象时，去看下ArrayList的构造函数，发现它的代码是这样的：
```
    /**
     * Constructs an empty list with an initial capacity of ten.
     */
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
```
而`elementData`和`DEFAULTCAPACITY_EMPTY_ELEMENTDATA `都是Object数组：
```
transient Object[] elementData; // non-private to simplify nested class access

private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
```
为啥在初始化时，要指向这个数组，是为了避免我们反复的创建无用数组，所有新new出来的ArrayList底层数组都指向缓存在方法区里的Object[]数组。
## 2.add添加元素
```
public boolean add(E e) {
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        elementData[size++] = e;
        return true;
    }
```
首先会执行`ensureCapacityInternal()`函数，看下这个函数
![](https://upload-images.jianshu.io/upload_images/6555928-197c0ee13d211b27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/6555928-56de7c527daf25be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/6555928-974b9f41ca72969a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
到这里我们发现执行了`Array.copyof()`函数，再看下这个函数的实现
![](https://upload-images.jianshu.io/upload_images/6555928-573e2f1daa0ee080.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
发现会调用`System.arraycopy`这个native方法，主要功能就是进行数组的拷贝，到目前是初始化了一个长度为10的数组，然后就到了下一步
![](https://upload-images.jianshu.io/upload_images/6555928-651ce0ca1677b942.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
将数组的第一个元素赋值e，然后size加一，然后add就操作完成了。
## 3.size()求大小
![](https://upload-images.jianshu.io/upload_images/6555928-19777c5e3f805ebe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这个size就是上一步的size，每添加一个元素都会加1，所以求大小只要把这个值返回就行
## 4.ArrayList扩容

上方说道，添加以一个元素的时候，会初始化一个长度为10的数组，那当长度超过10时，会进行什么操作呢？还是来看看add的源码
![](https://upload-images.jianshu.io/upload_images/6555928-b5bf1181b00cd6b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
和上方一样，还是会进到`ensureCapacityInternal()`中,但传入的值会是11
![](https://upload-images.jianshu.io/upload_images/6555928-3e1b6a59a4da2373.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这一步，会进入循环，将`minCapacity`的值赋11，然后执行将其作为参数传入`ensureExplicitCapacity()`
![](https://upload-images.jianshu.io/upload_images/6555928-5303ddb33269da5e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这一步没区别，来看下一步
![](https://upload-images.jianshu.io/upload_images/6555928-32efdbc9f8896bfc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这是重点，首先将`oldCapacity + (oldCapacity >> 1)`值赋给newCapacity。>>是位运算，>>多少位=除以2的多少次方。这个意思就是每次超出数组大小都会扩大原来的1/2。然后后面就和前面一样，就不详细阐述了。

