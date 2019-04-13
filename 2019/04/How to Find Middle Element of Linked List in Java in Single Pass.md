# How to Find Middle Element of Linked List in Java in Single Pass

> 如何只遍历一遍单链表找到中间的元素？大部分人常用的方法是先遍历一遍计算出单链表的长度，然后再从头向后一半的长度找到中间元素，那有没有什么办法可以只用遍历一次就找到呢？

## 1. 思路

我们可以通过两个指针来遍历链表，当前面的指针指向链表的末尾时，另外一个指针就刚好指向链表的中间元素，关键是如何确定这两个元素的步长呢？事实上这种思路可以解决许多类似的问题

首选我们来回顾一下单链表的特征，单链表的节点包含一个数据元素和一个地址元素，地址元素存储着下一个元素的地址，当地址元素为null的时候，这个节点即为尾节点。

**如果要第二个指针在第一个指针到末尾的时候刚好指向中间元素，则需要保证第一个指针每走两步，第二个指针才能走一步，即第二个指针只走一半的长度。**

## 2. 代码

```java
package com.liuyao;

public class Main {

    public static void main(String[] args) {
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(4);
        Node node5 = new Node(5);
        Node node6 = new Node(6);

        node1.next = node2;
        node2.next = node3;
        node3.next = node4;
        node4.next = node5;
        node5.next = node6;

        Node current = node1;
        int length = 1;
        Node middle = node1;
        while (current.next != null) {
            length++;
            if (length % 2 == 0) {
                middle = middle.next;
            }
            current = current.next;
        }
        System.out.println("The length is: " + length);
        System.out.println("The middle is: " + middle.num);

    }

    static class Node {
        private Integer num;
        private Node next;

        public Node(Integer num) {
            this.num = num;
        }

        public Integer getNum() {
            return num;
        }

        public void setNum(Integer num) {
            this.num = num;
        }

        public Node getNext() {
            return next;
        }

        public void setNext(Node next) {
            this.next = next;
        }
    }
}

```

输出结果为：

```
The length is: 6
The middle is: 4
```

如果不要node6的话，长度为奇数的话：

```
The length is: 5
The middle is: 3
```

