---
title: java面试题-基础篇
date: 2017-03-19 17:35:41
tags: java面试
categories: java面试
keywords: java面试,java基础
---
### 面向对象的特征：继承、封装和多态
* 继承：子类继承父类所有非私有的属性和方法，使得子类有父类的一些特性。
* 封装：把对象属性和操作包围起来，向外提供接口和操作的方法
* 多态：父类在运行的提现子类的属性和方法。
<!--more-->
### final, finally, finalize 的区别
* Final是属性或者方法的修饰词，表示子类不能修改和重写。
* Finally是try catch的最后必须操作的语句
* Finalize是gc必然会调用的方法。

### Exception、Error有何异同
* Exception是异常，表示程序编写有错误，有运行时异常和编译时异常。
* Error是错误，表示比较严重的错误，比如虚拟机方面的错误

### int 和 Integer 有什么区别，Integer的值缓存范围
* Int数字类型，Integer包装类，缓存范围-128-127
