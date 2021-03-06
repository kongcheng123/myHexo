---
title: JVM之判断对象的存活状态
date: 2017-11-05 17:53:24
tags:
- jvm
---
> jvm垃圾收集器在进行垃圾回收时，会判断对象是否存活状态，只有死去的对象才会被回收。那么怎么判断对象的存活状态呢？

1. 引用计数算法
  - 含义：给对象中添加一个引用计数器，每当有一个地方引用，计数器就加1；引用失效，计数器就减1；当计数器为0时，表示该对象不可能被使用。
 - 弊端：很难解决对象之间循环引用的问题
 - 引用类型：
   1. 强引用：只要强引用还在，就永远不会被回收
   2. 软引用：当要发生内存溢出时，该类对象才会被回收
   3. 弱引用：该类对象只能活到下次垃圾回收之前
   4. 虚引用：虚引用和生命周期没有关系。该类对象在任何时候都有可能被回收
2. 可达性分析算法
 - 含义：通过一系列的称为“GC Roots”的对象作为起始点，从这些节点向下探索，探索所走过的路径称为引用链，当一个对象到GC Roots没有任何引用链时，表示此对象不可用

 - ![](http://upload-images.jianshu.io/upload_images/6555928-beaab1bad75b9de2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 - 可作为GC Roots的对象类型：
   1. 虚拟机栈中引用对象
   2. 方法区中的类静态属性引用对象
   3. 方法区中常量引用对象
   4. 本地方法栈中native引用对象
3. finalize最终判断存活状态
- 原理：当可达性分析后，发现没有和GC Roots相连，该对象会**第一次**被标记，并筛选该对象是否有必要执行finalize()方法。筛选的条件是&nbsp;①没有覆盖finalize()方法，②finalize()方法已经被执行过。**就是说finalize()方法只能被执行一次**
有必要执行finalize()方法的对象，会被放在一个F-Queue的队列中，然后会有一个自动创建，低优先级的Finalizer线程执行。该执行过程不一定会结束。因为对象在执行过程中，可能执行缓慢，或发生死循环。接着，GC会对队列中的对象进行**第二次标记**，如果一个对象重新与引用链上的对象关联，那么该对象就会存活，否则会被回收。
