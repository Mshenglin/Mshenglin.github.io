---
title: java类集框架-HashSet和迭代器的使用
date: 2019-08-07 22:40:04
tags: java
categories: java类集
---

上一篇博客主要讲述了Collection接口中的List集合以及他的子类。今天说明一下Collection另外两个重要的子类Set和Queue。

<h3> Set集合与迭代器的使用</h3>
**Set与List都为Collection的子类,两者的不同点:**
+ Set集合不允许有重复的元素出现，而List允许有重复的元素出现。

-  Set集合是一个无序的集合(元素取出时的顺序与向其中添加时的顺序可能不同)，相反List是有序的一个集合(元素取出时的顺序与向其中添加时的顺序相同)。

<h4>**Set集合的子类**</h4>
---

**<1>HashSet**

HashSet

查阅HashSet集合的API介绍：此类实现Set接口，由哈希表支持（实际上是一个 HashMap集合）。HashSet集合不能保证的迭代顺序与元素存储顺序相同。

HashSet集合，采用哈希表结构存储数据，保证元素唯一性的方式依赖于：hashCode()与equals()方法。

哈希表是一种储存数据的数据结构。这在后面一段时间将会更新这里数据结构的内容。并且会更深层次的讲解HashSet如何实现储存的数据不重复。

下面根据具体的实例来讲解Set集合的使用
    
**1.当集合中存放的是基本数据包装类、String类、Date类等，本身覆写父类中的Object中的equal()与hashCode()，因此可以对其进行排序。**

 例子如下：
    
        package com.msl.diguo;
        
        import java.util.HashSet;
            public class SetDemo {
                public static void main(String[] args) {
                    Set<Integer> s=new HashSet<Integer>();  //根据多态性实例化HashSet对象
                    s.add(2);//向集合中添加元素
                    s.add(1);
                    s.add(3);
                    System.out.println(s);  [1,2,3]	/**toString()方法被重写，打印集合中的元素,
                                                        * 并且集合中的元素为储存时的不同*/
                                                        
                }        
            }

  **迭代器的使用**

   根据上面的例子，我们可以通过直接打印集合名称即可打印集合中所有的元素，
   原因是HashSet中的toString()方法被覆写，但是在我们实际的开发之中，
   通常使用Iterator类或者foreach输出集合中的元素。

   **Iterator**类提供的API

+ hahasNext()    返回 true如果迭代具有更多的元素。  
+ next()    返回迭代中的下一个元素。  
+ remove()     从基础集合中移除这个迭代器返回的最后一个元素（可选操作）。  
  

 遍历上面s集合中的元素

        package com.xu.msl.next;
        
        import java.util.HashSet;
        import java.util.Iterator;
        import java.util.Set;
        
        public class Demo {
        public static void main(String[] args) {
            Set<Integer> s=new HashSet<Integer>();  //根据多态性实例化HashSet对象
            s.add(2);//向集合中添加元素
            s.add(1);
            s.add(3);
            s.add(4);
            Iterator<Integer> iterator=s.iterator();//使用HashSet方法实例化一个迭代器
            while(iterator.hasNext()){	//判断是否有下一个元素		
            System.out.println(iterator.next());  //返回正在迭代的元素
        }                                      //打印结果 1，2，3，4
        }
        }

  第二种输出方式foreach语句

  代码如下
    
        package com.xu.msl.next;
        
        import java.util.HashSet;
        import java.util.Iterator;
        import java.util.Set;
        
        public class Demo {
        public static void main(String[] args) {
            Set<Integer> s=new HashSet<Integer>();  //根据多态性实例化HashSet对象
            s.add(2);//向集合中添加元素
            s.add(1);
            s.add(3);
            s.add(4);
            for(Integer set:s)
            {
                System.out.println(set);
            }
            
        }
        }

 根据上面的代码可以看出，相对于迭代器foreach语句更加简洁。

---
 **2.当集合中存放的是我们自定义的类时，我们要通过重写hashCode()和equal()方法保证元素的唯一性。**

 例子如下

自己定义的实体类

        package com.xu.msl.xxxx;
        
        public class Student {
        private  String name;
        private  int age;
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        public int getAge() {
            return age;
        }
        public void setAge(int age) {
            this.age = age;
        }
        public Student(String name, int age) {
            super();
            this.name = name;
            this.age = age;
        }
        public String toString() {
            return "Student [name=" + name + ", age=" + age + "]";
        }


​        
​        }

测试类

            package com.xu.msl.next;
            
            import java.util.ArrayList;
            import java.util.Collections;
            import java.util.HashSet;
            import java.util.Iterator;
            import java.util.List;
            import java.util.Set;
            
            public class Test {
                    public static void main(String[] args) {
                        Set<Student> s=new HashSet<Student>();
                        Student[] stu={new Student("D",20), //对象数组
                                new Student("D",20),
                                new Student("B",12),
                                new Student("A",40)
                        };
                        for(int i=0;i<stu.length;i++)   //向集合中添加元素
                        {
                            s.add(stu[i]);
                        }
                        Iterator<Student> iterator=s.iterator();
                        while(iterator.hasNext()){
                        System.out.println(iterator.next());
                        }

输出结果：

Student [name=B, age=12]

Student [name=A, age=40]

Student [name=D, age=20]

Student [name=D, age=20]

显然，在集合中出现了“相同”的元素，这时候我们应该覆写equal()和hashCode()方法来保证唯一性。

代码如下

实体类(在刚才的基础上重写了equal()与hashCode()方法)

        package com.xu.msl.next;
        
        public class Student {
        private  String name;
        private  int age;
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        public int getAge() {
            return age;
        }
        public void setAge(int age) {
            this.age = age;
        }
        public Student(String name, int age) {
            super();
            this.name = name;
            this.age = age;
        }
        public String toString() {
            return "Student [name=" + name + ", age=" + age + "]";
        }
        @Override
        public int hashCode() {
            final int prime = 31;
            int result = 1;
            result = prime * result + age;
            result = prime * result + ((name == null) ? 0 : name.hashCode());
            return result;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj)
                return true;
            if (obj == null)
                return false;
            if (!(obj instanceof Student))
                return false;
                else{
            Student other = (Student) obj;
            if (age != other.age)
                return false;
            if (name == null) {
                if (other.name != null)
                    return false;
            } else if (!name.equals(other.name))
                return false;}
            return true;
        }
        }

   **测试类**

        package com.xu.msl.next;
        
        import java.util.ArrayList;
        import java.util.Collections;
        import java.util.HashSet;
        import java.util.Iterator;
        import java.util.List;
        import java.util.Set;
        
        public class Test {
                public static void main(String[] args) {
                    Set<Student> s=new HashSet<Student>();
                    Student[] stu={new Student("D",20),
                            new Student("D",20),
                            new Student("B",12),
                            new Student("A",40)
                    };
                    for(int i=0;i<stu.length;i++)
                    {
                        s.add(stu[i]);
                    }
                    Iterator<Student> iterator=s.iterator();
                    while(iterator.hasNext()){
                    System.out.println(iterator.next());
                    }

  



  打印输出的结果

  Student [name=A, age=40]

  Student [name=B, age=12]

  Student [name=D, age=20]

  对比两次输出的结果，可以看出当我们覆写了equal()和hashCode()方法时，就可以保证对象的唯一性。

  <h4>Set的另外两个子类</h4>
  LinkedHashSet、TreeSet和Queue(队列)涉及到数据结构，这将会在后续更新数据结构时讲解。欢迎关注！

  

