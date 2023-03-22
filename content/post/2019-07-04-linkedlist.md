---
title:       '链表LinkedList'
date:        '2019-07-04'
description: ''
author:      'wmszhe'
image:       ''
tags:
    - 数据结构
    - 算法
categories:
    - 
---

<!--more-->

## 链表 LinkedList

### 定义

链表不需要一块连续的内存空间，它通过“指针”将一组**零散的内存块**串联起来使用

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/d5d5bee4be28326ba3c28373808a62cd.jpg)

其中，我们把内存块称为链表的“**结点**”。为了将所有的结点串起来，每个链表的结点除了存储数据之外，还需要记录链上的下一个结点的地址。我们把这个记录下个结点地址的指针叫作**后继指针 next**

### 一. 常见的链表结构

#### 1. 单链表	Singly linked list

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/b93e7ade9bb927baad1348d9a806ddeb.jpg)

有两个结点是比较特殊的，它们分别是第一个结点和最后一个结点。我们习惯性地把第一个结点叫作**头结点**，把最后一个结点叫作**尾结点**。其中，头结点用来记录链表的基地址。有了它，就可以遍历得到整条链表。而尾结点特殊的地方是：指针不是指向下一个结点，而是指向一个**空地址 NULL**，表示这是链表上最后一个结点

##### 1.1插入、删除、查找

数组的插入、删除操作时，为了保持内存数据的连续性，需要做大量的数据搬移，所以时间复杂度是 O(n)。而在链表中插入或者删除一个数据，并不需要为了保持内存的连续性而搬移结点，因为链表的存储空间本身就不是连续的。所以，在链表中插入和删除一个数据是非常快速的,时间复杂度是 O(1)。但是，链表要想随机访问第 k 个元素，就没有数组那么高效了。因为链表中的数据并非连续存储的，所以无法像数组那样，根据首地址和下标，通过寻址公式就能直接计算出对应的内存地址，而是需要根据指针一个结点一个结点地依次遍历，直到找到相应的结点。时间复杂度是 O(n)

> 插入删除时间复杂度O(1)

> 查找时间复杂度O(n)

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/452e943788bdeea462d364389bd08a17.jpg)

#### 2. 循环链表	Multiply linked list

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/86cb7dc331ea958b0a108b911f38d155.jpg)

**循环链表是一种特殊的单链表**。它跟单链表唯一的区别就在尾结点。单链表的尾结点指针指向空地址，表示这就是最后的结点了。而循环链表的尾结点指针是指向链表的头结点。

#### 3. 双向链表	Doubly linked list

![](https://raw.githubusercontent.com/wmszhe/pichub/master/imgs/cbc8ab20276e2f9312030c313a9ef70b.jpg)

单向链表只有一个方向，结点只有一个后继指针 next 指向后面的结点。而双向链表，顾名思义，它支持两个方向，每个结点不止有一个后继指针 next 指向后面的结点，还有一个前驱指针 prev 指向前面的结点。

双向链表需要额外的两个空间来存储后继结点和前驱结点的地址。所以，如果存储同样多的数据，双向链表要比单链表占用更多的内存空间。虽然两个指针比较浪费存储空间，但可以支持双向遍历，这样也带来了双向链表操作的灵活性。



### 二. 经典的链表应用场景

LRU 缓存淘汰算法

##### 2.1 实现原理

维护一个有序单链表，越靠近链表尾部的结点是越早之前访问的。当有一个新的数据被访问时，我们从链表头开始顺序遍历链表。

1. 如果此数据之前已经被缓存在链表中了，我们遍历得到这个数据对应的结点，并将其从原来的位置删除，然后再插入到链表的头部。
2. 如果此数据没有在缓存链表中，又可以分为两种情况：
    - 如果此时缓存未满，则将此结点直接插入到链表的头部
    - 如果此时缓存已满，则链表尾结点删除，将新的数据结点插入链表的头部

### 三. 常见的链表算法

1. 单链表反转

```
fun main() {
    val note1 = SinglyLinkedNote(1)
    val note2 = SinglyLinkedNote(2)
    val note3 = SinglyLinkedNote(3)
    val note4 = SinglyLinkedNote(4)

    note1.next = note2
    note2.next = note3
    note3.next = note4

    printNode(reverseSingleLinkedList(note1))
}

/**
 * 单链表反转
 * @param node 单链表
 * @return 反转后的结果
 */
fun reverseSingleLinkedList(node: SinglyLinkedNote?): SinglyLinkedNote? {
    if (node?.next == null) {
        return node
    }
    val linkedNote = reverseSingleLinkedList(node.next)
    node.next?.next = node
    node.next = null
    return linkedNote
}

/**
 * 单链表
 */
class SinglyLinkedNote(var value: Int?) {
    var next: SinglyLinkedNote? = null
}

/**
 * 打印链表
 * @param data 链表
 * @return 链表数据 eg: { 1 2 3 4 }
 */
fun printNode(data: SinglyLinkedNote?) {
    var node: SinglyLinkedNote? = data
    val str: StringBuilder = StringBuilder("{ ")
    while (node != null) {
        str.append(node.value).append(" ")
        node = node.next
    }
    str.append("}")
    println(str.toString())
}
```

2. 链表中环的检测

```

```

3. 两个有序的链表合并

```

```

4. 删除链表倒数第 n 个结点

```

```

5. 求链表的中间结点

```

```

