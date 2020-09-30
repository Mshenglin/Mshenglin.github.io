---
title: String,StringBuffer与StringBulider的联系与区别
tags:  java基础
categories: java基础
date: 2019-11-19 20:28:27
---
首先大概讲述一下java中的数据类型，java的数据类型分为基本数据类型和引用数据类型。基本数据类型：int(整形)、short(短整型)、long(长整型)、boolean(布尔型)、char(字符型)、byte(字节型)、float(浮点型)、double(双精度浮点型)。引用类型分为数组，类(class)和接口(interface)。

---

<h5>>String,StringBuffer与StringBulider的联系</h5>
String，StringBuffer与StringBulider三者都是是java提供的类，因此他们的数据类型为引用数据类型，这三者都提供了对字符串操作的方法。既然他们的功能都是对字符串进行操作，为什么还有设计三个类呢？下面谈一谈他们的区别。

---

<h5>>String,StringBuffer与StringBulider的区别</h5>
---


**String类型一旦声明他的值是无法修改的**

当我们对一个字符串进行操作时，就会在内存中重新开辟一片空间出来用来储存产生的新的字符串。这样大大的浪费了空间。

举个例子，代码如下：
        package org.xu.msl.string;

        public class StringDemo {
        public static void main(String[] args) {
            String string="my name is ";	//该过程开辟一次空间用来储存string
            string=string+"string";//该过程共开辟两次空间，一次用来储存字符串string,另一次用来储存拼接后的字符串，并将储存str的地址指向最后一次开辟的空间地址
        }
        }

因此当我们要对字符串本身进行操作时为了节省内存的资源，就会使用StringBuffer和StringBulider类，这两种类对字符串本身进行操作时不会产生新的对象，相对于String类，JDK中StringBuffer和StringBulider类中提供了更加多的方法用来操作字符串。同样是字符串的拼接方法。StringBuffer与StringBulider可以直接调用append()方法，并且不会开辟新的内存空间。

代码如下：

        package org.xu.msl.string;
    
        public class StringDemo {
        public static void main(String[] args) {
            StringBuffer str=new StringBuffer("my name is ");	//实例化一个StringBuffer对象并对其赋值
                str.append("StringBuffer");//向字符串会追加字符，此过程不会开辟新的内存空间
                System.out.println(str);
        }
    
        }

StringBuffer与StringBulider的区别

StringBuffer与StringBulider很大一部分是相同的，包括他们提供的方法。他们的区别主要在于：StringBulider执行效率高但不安全，StringBuffer执行的效率低但安全。

**小结**

>（1）如果要操作少量的数据用 String；

>（2）多线程操作字符串缓冲区下操作大量数据 StringBuffer； 。

>（3）单线程操作字符串缓冲区下操作大量数据 StringBuilder（推荐使用）。