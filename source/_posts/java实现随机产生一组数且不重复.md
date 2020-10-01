---
title:  通过java实现，随机产生一组数据且不重复
tags:   [java]
categories:  java基础
date:  2019-08-20 20:39:00
---
<h2>引言</h2>
由于我最近在学习java语言，所以本篇文章将通过java实现一个在一组已知的数据中，在其中随机抽取一组数据且不重复。来巩固自己的学习知识。
***
  <h3>思路分析</h3>
首先，我们需要通过一个容器来储存已知的数据，然后通过Random类实现随机数，最后再通过代码找到符合的的数据，最终输出这一组数据。
******
<h4>实现方法</h4>
<h5>1.通过数组的方式实现</h5>
**代码如下**

    package org.xu.msl.xxx;
    import java.util.Random;
    public class RandomDemo {
        public static void main(String[] args) {
            int[] a={1,2,3,4,5,6,7,8,9,10,11};  //初始化一组已知的数组
            int[] a1=new int[5];//定义一个接受数组
            Random r=new Random();  //实例化一个Random对象
            for(int i = 0;i<a1.length;i++)
            {
                int temp=r.nextInt(a.length);
                a1[i]=a[temp];      //随机产生a[]的下标值，并将该值赋值给接受数组                
                a[temp]=0;	
                a=change(a);    //移除a[]数组中赋值过的数据
            }
            for(int i = 0;i<5;i++)
            {
                System.out.print(a1[i]+"\t");
            }
        }
        public static int[] change(int aar[]){
            int[]  temp=new  int[aar.length-1];
            int n=0;
            for(int i=0;i<aar.length;i++)   //通过循环筛选没有赋值过的数据并赋值
            {	
                if(aar[i]!=0)
                {
                    temp[n++]=aar[i];
                }
            }
            return temp;       //返回一个新的数组
        }
    }


<h5>2.通过List集合实现</h5>
**代码如下**


        package org.xu.msl.xxxx;
        import java.util.ArrayList;
        import java.util.List;
        import java.util.Random;
        import java.util.Scanner;
    
        public class LIstDemo01 {
    
            public static void main(String[] args) {
                List<Integer>  a=new ArrayList<Integer>();	//初始化一个整型的List集合
                List<Integer>  b=new ArrayList<Integer>();//初始化一个整型的List集合。用来接受数据
                Random r=new Random();	//实例化一个Random对象
                for(int i=1;i<=20;i++)
                {
                    a.add(i);		//对该集合进行赋值
                }
                    for(int i=0;i<10;i++)
                    {
                        int s=a.remove(r.nextInt(a.size()));	//随机取出一个a中的数据并将其移除并返回值赋值给s
                        b.add(s);			
                    }
                System.out.println(b);
            }
        }

<h5>总结</h5>
    通过这个小练习，主要熟悉List类集中ArrayList的操作以及Random类的使用。由于本人是一个初学者，水平有限，读者可以将代码自行进行优化以及功能的扩充。