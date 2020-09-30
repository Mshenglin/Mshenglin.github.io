---
title: 剑指offer--链表篇
date: 2020-03-26 08:32:30
tags: 数据结构与算法
categories:	算法
---

## 剑指offer链表篇

### 概述

这篇文章主要将剑指offer中与链表相关的题目.目录如下

[TOC]



### 06.从尾到头打印链表

[leetcode](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

#### 题目描述

从尾到头反过来打印每一个节点的值

原链表：1-->2-->3

输出样例：3，2，1

#### 解题思路

##### 一 使用栈实现

```java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
import java.util.Stack;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        //用来存储遍历以后的数据
        ArrayList<Integer> arr=new ArrayList<>();
        //创建一个栈，利用栈的特性，储存数据
        Stack<Integer> stack=new Stack<>();
        //遍历链表，将数据存储在栈中
        while(listNode!=null){
            stack.push(listNode.val);
            listNode=listNode.next;
        }
        //将数据从栈中取出，并存入list中
        while(!(stack.isEmpty())){
            arr.add(stack.pop());
        }
              return arr;
              }
              }
```

##### 二 使用双指针迭代

https://leetcode-cn.com/problems/reverse-linked-list/solution/dong-hua-yan-shi-206-fan-zhuan-lian-biao-by-user74/

leetcode 反转链表题解相似，不过这样会改变链表结构。

```java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> arr=new ArrayList<>();
        ListNode pre=null;
        ListNode cur=listNode;
        while(cur!=null){
            ListNode tmp=cur.next;
            cur.next=pre;
            pre=cur;
            cur=tmp;
        }
        while(pre!=null){
            arr.add(pre.val);
            pre=pre.next;
        }
        return arr;
    }
}
```

##### 使用递归

将链表递归，然后存储返回的元素

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    //初始化数组用
    int[] a;
    int i;
    int j;
    public int[] reversePrint(ListNode head) {
         ListNode cur=solve(head);
         return a;
    }
    public ListNode solve(ListNode head){
        //递归终止条件
         if(head==null){
             a=new int[i];
             return head; 
         }          
        //初始化数组容量          
        i++;
        //储存元素
        ListNode node=solve(head.next);
         a[j]=head.val;
         j++;
         node=head;
         return node;
    }
}
```

### 18.删除链表的一个节点

[leetcode](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

该题为对链表的最基本操作。

#### 题目描述

```
给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

注意：此题对比原题有改动

示例 1:
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.

示例 2:
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.

```

#### 解题思路

##### 思路一

遍历链表在符合条件的前一个节点停止，然后对其操作。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        //使用虚拟头节点
        ListNode cur=new ListNode(-1);
        //将虚拟头节点next指向head
        cur.next=head;
        //保存头节点用来返回
        ListNode node=cur;
        //在链表中查找与符合条件的节点，并在节点的头一个节点停止
        while(cur!=null){
            if(cur.next.val==val){
                 cur.next=cur.next.next;
                break;
            }
            else
            cur=cur.next;
        }
       return node.next; 
    }
}
```

##### 思路二 使用双指针

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        //使用虚拟头节点
        ListNode dun=new ListNode(-1);
        //将虚拟头节点next指向head
        dun.next=head;
        //cur快指针，per慢指针
        ListNode pre=dun;
        ListNode cur=head;
        ListNode node=dun;
        //在链表中查找与符合条件的节点，并在节点的头一个节点停止
        while(cur.val!=val&&cur!=null){
            pre=cur;
            cur=cur.next;
        }
        pre.next=cur.next;
       return node.next; 
    }
}
```

### 22.链表中倒数第k个元素



[leetcode](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

#### 题目表述

```java
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。
示例：

给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.

```

#### 解题思路

使用双指针，构建步长，返回慢指针。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
       //使用双指针，构建步长然后一起向后遍历，返回慢指针后的元素
       if(head==null){
           return null;
       }
       //慢指针
       ListNode cur=head;
        //快指针
        ListNode pre=head;
        int i=0;
        while(pre!=null){
            //构建步长
            if(i<k){
                pre=pre.next;
                i++;
            }
            else{
                pre=pre.next;
                cur=cur.next;
            }
        }
        return cur;
    }
}
```

### 23.链表中环的入口节点

[nowcoder](https://www.nowcoder.com/practice/253d2c59ec3e4bc68da16833f79a38e4?tpId=13&tqId=11208&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

#### 解题思路

该题为技巧题。

https://zhuanlan.zhihu.com/p/103626709

两个重要结论

- **设置快慢指针，假如有环，他们最后一定相遇在环中。**
- **两个指针相遇后，让两个指针分别从链表头和相遇点重新出发，每次走一步，最后一定相遇于环入口。**

#### 代码实现

```java
/*
 public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
*/
public class Solution {

    public ListNode EntryNodeOfLoop(ListNode pHead)
    {
        if(pHead==null||pHead.next==null){
            return null;
        }
        //left是快指针，right是慢指针
        ListNode left=pHead.next;
        ListNode right=pHead.next.next;
        //当两个指针相遇的时候，结束循环
        while(left!=right){
            if(left==null){
                return null;
            }
            left=left.next;
            right=right.next.next;
        }
        ListNode a=pHead;
        while(a!=left){
            a=a.next;
            left=left.next;
        }
        return left;
    }
}
```

### 24.反转链表

[leetcode](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

#### 题目描述

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL

#### 解题思路

##### 思路一 使用队列，将链表中的元素都存入队列中，然后取出连接

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        //创建一个队列
       Queue<Integer> queue=new LinkedList<Integer>();
       //判断特殊情况
        if(head==null)
        return null;
        //遍历链表，存入队列中
        while(head!=null) 
        {
             queue.add(head.val);
            head=head.next;
        }
        //取出队列中的元素，并，连接新链表
        int num= queue.poll();
        ListNode list=new ListNode(num);
        while(!queue.isEmpty())
        {
             num= queue.poll();
            ListNode down=new ListNode(num);
            down.next=list;
            list=down;
            
        }
        return list;
    }
}
```

#### 思路二 使用双指针原地反转

https://leetcode-cn.com/problems/reverse-linked-list/solution/dong-hua-yan-shi-206-fan-zhuan-lian-biao-by-user74/

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        //如果看不懂直接看链接动画
 		//建立两个指针
        ListNode pre=null;
        ListNode cur=head;
        while(head!=null){
            cur=head.next;
            head.next=pre;
            pre=head;
            head=cur;
        }
        return pre;
    }
}
```

#### 思路三 使用递归

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
    //递归的终止条件
        if(head==null||head.next==null){
            return head;
        }
        //该值一直没有变，就是链表的最后一个节点
        ListNode cur=reverseList(head.next);
        head.next.next=head;
        //成环，head.next=null;
        head.next=null;
        return cur;
    }
}
```

### 25.合并两个排序链表

[leetcode](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

#### 题目描述

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
限制：

0 <= 链表长度 <= 1000

#### 解题思路

##### 思路一 使用递归

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
            if(l1==null||l2==null){
                return l1==null?l2:l1;
            }
            if(l1.val<=l2.val){
                //如果l1的值比l2的小，则让l1.next与l2继续比较
                l1.next=mergeTwoLists(l1.next,l2);
                return l1;
            }
            else{
                // //如果l2的值比l1的小，则让l2.next与l1继续比较
                l2.next=mergeTwoLists(l2.next,l1);
                return l2;
            }
    }
}
```

##### 思路三：迭代

https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        //创造虚拟头节点
        ListNode dump=new ListNode(-1);
        //保存改虚拟节点，用来返回值
        ListNode node=dump;
        //当l1和l2都不为null的时候
        while(l1!=null&&l2!=null){
            //l1的值大于l2
            if(l1.val<l2.val){
                dump.next=l1;
                l1=l1.next;
            }
            else{
                dump.next=l2;
                l2=l2.next;
            }
            //更新dump的位置
            dump=dump.next;
            }
            dump.next=l1==null?l2:l1;
        return node.next;
    }
}
```

### 35.复杂链表的复制

[leetcode](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

#### 解题思路 使用哈希表

将链表遍历一遍，将已有链表作为键，新创建的节点为值，存入哈希表，第二次遍历取出值，并对他们的next和random指针赋值

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        if(head==null){ 
            return null;
        }
        //创建一个哈希表
        HashMap<Node,Node> map=new HashMap<>();
        //保存头节点
        Node cur=head;
    while(cur!=null){
        //将当前节点和一个新的空节点存入map中
        map.put(cur,new Node(cur.val));
        cur=cur.next;
    }
    //将map中的通过key组织value结构
    Node newnode=map.get(head);
    while(head!=null){
        //取出链表中的值，并赋值
        Node node=map.get(head);
        node.next=map.get(head.next);
        node.random=map.get(head.random);
        head=head.next;
    }
    return newnode;
    }
}
```

### 52.两个链表的第一个公共节点

[leetcode](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

#### 题目描述

输入两个链表，找出它们的第一个公共节点。

如下面的两个链表**：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

在节点 c1 开始相交。

 **示例 1：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```java
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```

**示例 2：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_2.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```

**示例 3：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_3.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
```

注意：

如果两个链表没有交点，返回 null.
在返回结果后，两个链表仍须保持原有的结构。
可假定整个链表结构中没有循环。
程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。
本题与主站 160 题相同：https://leetcode-cn.com/problems/intersection-of-two-linked-lists/

#### 解题思路

链表一的长度是L1+C，链表二的长度是L2+C，第一个人走了L1+C步后，回到第二个人起点走L2步；第2个人走了L2+C步后，回到第一个人起点走L1步。 当两个人走的步数都为L1+L2+C时就两个家伙就相爱了。当两个链表不相交同时指向null，循环也可以退出。

https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/solution/shuang-zhi-zhen-fa-lang-man-xiang-yu-by-ml-zimingm/

#### 代码实现

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        //储存两个头节点
        ListNode a=headA;
        ListNode b=headB;
        //当两个链表的节点相同的时候，退出循环
            while(headA!=headB){
                //当链表A遍历完时，赋值在b的链表头
                if(headA==null){
                    headA=b;
                }else
                {
                 headA=headA.next;
                }
                //当链表B遍历完时A，赋值在A的链表头
                if(headB==null){
                    headB=a;
                }
                else
                headB=headB.next;
            }
            //如果相遇，返回一个即可，不相遇值都为null
            return headA;
    }
}
```

