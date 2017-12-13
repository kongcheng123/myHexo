---
title: 浅谈设计模式一之单例模式
date: 2017-10-01 09:12:51
tags:
- 设计模式
---

## 1. 概念
  一个实现`Singleton`类一般拥有以下两个方法,构造函数`Singleton()`，以及获取实例的方法`GetInstance()`。如下图所示：

![单例结构图.png](http://upload-images.jianshu.io/upload_images/6555928-61de04855cd4e5c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  需要注意的是，**构造方法`Singleton()`要私有化（用private修饰）,获取实例的方法`GetInstance()`要设置为静态（static）。**

## 2. 实现方法
- 懒汉式
```
//懒汉式单例类.在第一次调用的时候实例化自己   
public class Singleton {  
    private Singleton() {}  
    private static Singleton single=null;  
    //静态工厂方法   
    public static Singleton getInstance() {  
         if (single == null) {    
             single = new Singleton();  
         }    
        return single;  
    }  
}  
```
- 恶汉式
```
//饿汉式单例类.在类初始化时，已经自行实例化   
public class Singleton1 {  
    private Singleton1() {}  
    private static final Singleton1 single = new Singleton1();  
    //静态工厂方法   
    public static Singleton1 getInstance() {  
        return single;  
    }  
} 
```
## 3. 多线程时的单例模式
在多线程时，一般采用双重锁定的方式来实现单例模式
```
public static Singleton getInstance() {  
        if (singleton == null) {    
            synchronized (Singleton.class) {    
               if (singleton == null) {    
                  singleton = new Singleton();   
               }    
            }    
        }    
        return singleton;   
    }
```
