---
title: 入门JDBC---使用Java实现数据库的基本操作
tags: java
categories: java基础
date: 2019-09-25 17:14:00
---



<h5>初识JDBC</h5>
   JDBC官方解释为java连接数据库技术(Java Database Connectivity),是一种用于执行SQL语句的Java API，可以为多种关系数据库提供统一访问，它由一组用Java语言编写的类和接口组成。

   下面是个人对JDBC的理解，首先java是一种编程语言，数据库是用来储存电子数据处所。当我们通过java对数据库进行操作时，java语言本身不具有这个功能。为了可以实现Java对数据库的操作，就产生了JDBC。举个例子，比如，我们日常的插U盘操作，U盘与电脑本身没有什么关系。但是当我们要读取U盘中的内容时，必须要通过USB接口来操作，此时的USB接口就相当于JDBC。为两者建立联系。下面类比电脑读取U盘数据来讲解java连接数据库并对其中的数据进行基本的操作。

---
<h5>使用JDBC访问数据库的步骤</h5>
**1. 加载驱动**

   当我们插入U盘到电脑上时，电脑首先会进行加载驱动，在这里也是相同的。首先，我们要导入不同数据库的数据库驱动程序(JDK中不包含该功能)。驱动程序包如下,链接：https://pan.baidu.com/s/1Lt01o-xU0pMZo8374EZAcA 提取码：2om1，也可到mysql官网自行下载。然后将应用程序导入项目文件(这个大家自行搜索，百度教程非常详细)。

   代码如下：
       Class.forName("com.mysql.jdbc.Driver");

**2，创建连接对象对象**

   加载完驱动后就相当于电脑识别了你插入的是U盘。然后你的电脑上会会显示你的U盘信息。这个过程就相当于创建连接对象。具体实现方法如下，通过DriverManager类创建链接对象。

   代码：

   Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/数据库名称", "用户名", "用户密码");

**3.创建语句处理对象并对数据库进行操作**

   这一步相当如我们对U盘中的文件进行操作。

   创建语句处理对象

   代码如下：
    Statement stm=con.createStatement();

   对数据库中表进行更新操作

   代码如下：
    String sql="其中书写sql语句";
     stm.executeUpdate(sql);

   对数据进行查询工作

   代码如下：
    String sql="其中书写sql语句";
     stm.executeQuery(sql);
     
 **5.关闭数据库连接**

---

   具体代码如下：

            package org.xu.msl.jdbc;
    
        import java.sql.Connection;
        import java.sql.DriverManager;
        import java.sql.ResultSet;
        import java.sql.SQLException;
        import java.sql.Statement;
    
        public class Test {
          public static void main(String[] args) throws Exception {
                    //加载驱动	        
                    Class.forName("com.mysql.jdbc.Driver");
                    //注册驱动，链接Connection
                    Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/dbbank","root","root");
                    //验证数据库是否连接成功
                    System.out.println(con);
                    //创建语句处理对象
                    Statement stml=con.createStatement();
                    //对数据库中的数据进行增加操作
                    String sql="insert into users values(4,'王五','123','123456',9000)";
                    stml.executeUpdate(sql);
                    String sql1="insert into users values(3,'李四','1234','123456',8000)";
                    stml.executeUpdate(sql1);
                    //修改操作
                    String sq2="update users set u_card='1234' where u_id=2";
                    stml.executeUpdate(sq2);
                    //删除操作
                    String sql3="delete  from users where u_id=1";
                    stml.executeUpdate(sql3);
                    //查找操作
                    String aql4="select * from users";
                    ResultSet rult = stml.executeQuery(aql4);
                    while(rult.next()){
                        System.out.println("序列号："+rult.getInt("u_id")+"，姓名："+rult.getString("u_name")+"卡号"+rult.getString("u_card")+"密码："+rult.getString("u_pass")+"" +
                                ""+"余额"+rult.getString("u_money"));
                    }
                    //关闭数据库连接
                    if(rult != null)
                    {
                        rult.close();
                        }
                    if(stml != null)
                    {
                        stml.close();
                    }
                    if(con != null)
                    {
                        con.close();
                    }
          }         
        }       
**数据库表结构**
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| u_id    | int(11)     | NO   | PRI | NULL    |       |
| u_name  | varchar(20) | NO   |     | NULL    |       |
| u_card  | varchar(20) | NO   |     | NULL    |       |
| u_pass  | varchar(20) | NO   |     | NULL    |       |
| u_money | double      | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+