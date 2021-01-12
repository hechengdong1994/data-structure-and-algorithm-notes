# merge-two-sorted-lists

https://leetcode-cn.com/problems/merge-two-sorted-lists/

## 1 迭代

算法流程：

1. 依次循环比较两个链表中的第一个元素，将值较小的元素作为结果链表的后继节点，直至遍历完某一个链表
3. 将另一个还未遍历完的链表的第一个节点接入结果链表的后继节点

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    // 声明一个节点，作为返回结果的前驱节点
    ListNode result = new ListNode();
    // 声明一个节点，指向当前已处理完的节点
    ListNode current = result;
    // 当两个链表中都含有元素时，需要循环进行比较
    for (; l1 != null && l2 != null; ) {
        if (l1.val <= l2.val) {
            // 将结果链表的当前节点的后继节点指向值较小的节点
            current.next = l1;
            // 该链表的节点指针后移
            l1 = l1.next;
        } else {
            current.next = l2;
            l2 = l2.next;
        }
        // 结果链表的节点指针后移
        current = current.next;
    }
    // 将较长的链表的多余元素补上
    if (l1 != null) {
        current.next = l1;
    } else if (l2 != null) {
        current.next = l2;
    }
    return result.next;
}
```

该方法的时间复杂度为O(m+n)，其中m、n分别为两个链表的长度。空间复杂度为O(1)，因为只声明了额外的一个节点和指针。

2 递归