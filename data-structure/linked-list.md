# 链表

## 1 简介

链表是一维的、线性的数据结构，用来存储一组类型相同的数据。与数组不同，链表使用不连续的内存空间来存储每个数据，并通过指针将它们连接起来。通过指针指向可以访问到链表中的元素。

## 2 操作及时间复杂度

### 随机访问

由于链表使用不连续内存空间+指针的存储方式，当根据索引访问数据时，需要从头节点开始，逐个访问链表的每个元素，直到访问到指定索引的元素。因此链表的随机访问操作的时间复杂度为O(n)。

### 插入

将数据插入链表中的非尾部位置，与数组相反，不需要将该位置的后续元素全部后移一位，只需要修改前后节点的指针指向即可。因此链表的数据插入时间复杂度为O(1)。

### 修改

修改链表中指定下标的数据时，需要先通过随机访问方式查找到该数据，再进行数据替换。因此链表的数据修改时间复杂度为O(n+1)，即O(n)。

### 删除

与数据插入操作相同，从链表中删除数据，不需要将后续的元素全部前移一位。因此链表的数据删除时间复杂度为O(1)，即O(1)。

综上可以看出，链表和数组互相弥补了对方的不足，但也在对方的优势上付出了额外的性能代价。它们是两种互补的数据结构。

## 3 相关问题

[21.merge-two-sorted-lists](../leetcode/0021-merge-two-sorted-lists.md)

[206.reverse-linked-list](../leetcode/0206-reverse-linked-list.md)

[24.swap-nodes-in-pairs](../leetcode/0024-swap-nodes-in-pairs.md)

[141.linked-list-cycle](../leetcode/0141-linked-list-cycle.md)

[142.linked-list-cycle-ii](../leetcode/0142-linked-list-cycle-ii.md)

 [25.reverse-nodes-in-k-group](../leetcode/0025-reverse-nodes-in-k-group.md)