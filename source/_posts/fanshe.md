---
title: Java反射
date: 2017-10-12 14:46:10
tags:
- java
categories:
- java
---
> 最近在研究spring框架，而spring的ioc是基于反射机制来完成的，因此先来学习下反射

## 1. 使用场景
  当我们的程序在运行时，需要动态的加载一些类，而这些类可能由于之前用不到所以没有加载到jvm，而是在运行时根据需要才加载，比如，我们之前连接mysql时，都要动态的加载mysql驱动程序，这时就要用到反射。

## 2. 原理机制
 - java文件会被被编译成class文件
 - 通过class文件名获取这个文件
 - 调用newInstance动态的创建这个类

## 3. 实现
  - 获取class文件(三种方法)
     1. Class.forName
     2. 对象.getClass
     3. 对象.class 
  - 创建对象
    调用newInstance()方法
  - 获取对象参数
     1. getFiled: 访问公有的成员变量
     2. getDeclaredField：所有已声明的成员变量。但不能得到其父类的成员变量
  - 调用对象方法
      1. getDeclaredMethods()方法返回类或接口声明的所有方法，包括公共、保护、默认（包）访问和私有方法，但不包括继承的方法。
      2.getMethods()方法返回某个类的所有公用（public）方法，包括其继承类的公用方法。

## 4. 实例
``` 
public class testReflection {

    public int age=10;
    public int getAge(){
        return age;
    }
    public int getSome(int i){
        return i;
    }

    public static void main(String[] args) throws Exception{
        Class<?> clazz=Class.forName("xy.reflection.testReflection");
        //无参方法
        Method method=clazz.getMethod("getAge");
        int i=(Integer) method.invoke(clazz.newInstance());
        System.out.println(i+"");
        //有参方法
        Method m=clazz.getMethod("getSome", int.class);
        int j=(Integer) m.invoke(clazz.newInstance(),100);
        System.out.println(j+"");
    }

    @Test
    public void testMethod() throws Exception{
        Class<?> clazz=Class.forName("xy.reflection.testReflection");
        System.out.println(clazz.getName());
       //获取对象的属性
        Field field=clazz.getDeclaredField("age");
        field.set(this,2);
        System.out.println(age+"");

    }
}
  ```
