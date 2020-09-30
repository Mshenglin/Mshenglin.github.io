---
title: java类集框架总结-结构梳理与List集合
date: 2019-08-03 15:33:15
tags: java基础
categories: java类集
---

数据结构是以某种形式将数据组织在一起的集合，它不仅存储数据，还支持访问和处理数据的操作。Java提供了几个能有效地组织和操作数据的数据结构，这些数据结构通常称为Java集合框架。学习这些集合框架可以让我们大大的提高我们的开发效率。接下来就讲解一些常用的类集框架。

<h3>类集框架的结构</h3>
**常用类集框架结构**

![](1.jpg)


根据图片看出在java类集中，一共有两大接口：Collection与Map。Collection接口三个子类，分别为List、Set与Queue。Map的子类有两个HashMap与TreeMap。在我们实际的应用时，用的一般都时使用子接口。

**类集框架关系图**

![](2.jpg)

<h4>List集合</h4>
**List集合的特征**

>1. 所有的List中只能容纳单个不同类型的对象组成的表，而不是Key－Value键值对。例如：[ 1,c]；
>2. 所有的List中可以有相同的元素，例如Vector中可以有 [ tom,koo,too,koo ]；
>3. 所有的List中可以有null元素，例如[ tom,null,1 ]；
>4. 基于Array的List（Vector，ArrayList）适合查询，而LinkedList（链表）适合添加，删除操作。

<h5>List子类———ArrayList</h5>
Arraylist是基于数组实现的。相对于数组ArrayList的优点就是可以实现动态性，容量是可变的。

**ArrayList的使用方法**

实例化一个ArrayList的声明方式

        ArrayList<Integer> s=new ArrayList<Integer>();
        List<Integer> s1=new ArrayList<Integer>();  //利用多态性

ArrayList的构造方法
       
ArrayList()    构造一个初始容量为10的空列表 
ArrayList(int a)    构造一个初始容量为a的空列表

ArraySet常用的方法

+ add() 向列表中添加元素
+ clear() 移除该列表中的所有元素
+  remove(int index)  移除此列表中指定位置的元素。  
+ remove(Object o) 从该列表中移除指定元素的第一个发生，如果它是存在的。  
+ isEmpty()  判断该列表是否为空

<h5>List子类——Vecotor</h5>
Vecotor类与ArrayList都是基于数组实现的。他们的使用非常类似。这里就不重复了。这里ArrayList与Vecotor的不同，Vecotor是同步的，因此线程安全。相反ArrayList更适合单线程。

<h5>List子类——LinkedList</h5>
LinkedList使用与其他两个也是雷同，大家可以通过jdk查看他的ApI。

优缺点及特点

(1).Linkedlist相对于其他两个子接口他是基于链表实现的。他的优点是进行增删该用时短，缺点是查找会用时更长。(2)LinkedList不能实现同步，线程是不安全的。

**下一篇将会更新Set集合与迭代器的使用**