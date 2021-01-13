# reverse-linked-list

https://leetcode-cn.com/problems/reverse-linked-list/

## 1 迭代

算法流程：

1. 初始化：前一个元素为null，当前元素为head元素
2. 遍历链表
   3. 临时保存temp=当前元素的next元素
   2. 将当前节点的next指向前一个元素
   3. 更改当前元素引用=temp

```java
public ListNode reverseList(ListNode head) {
    // 遍历初始化
    ListNode prev = null;
    ListNode current = head;
    // 遍历链表
    while (current != null) {
        // 临时保存当前节点的后继节点，因修改指向后该节点丢失
        ListNode temp = current.next;
        // 翻转节点后继节点指向
        current.next = prev;
        // 指针后移
        prev = current;
        current = temp;
    }
    // 最终返回的是prev节点，因此时current为null
    return prev;
}
```

该方法的时间复杂度为O(n)，其中n为链表的长度。空间复杂度为O(1)。

### 1.1 空间优化

该优化方法利用了参数head，减少声明了一个额外变量。

```java
public ListNode reverseList(ListNode head) {
    ListNode current = null;
    while (head != null) {
        // 暂存下一节点
        ListNode next = head.next;
        // 翻转当前节点的后继节点指向
        head.next = current;
        // 指针后移
        current = head;
        head = next;
    }
    return current;
}
```

时间与空间复杂度相同。从执行结果看，因为少申请了一个ListNode对象，因此该方法内存消耗有降低。

## 2 递归

```java
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    // reversedHead指向的是原链表的最后一个元素，作为最终的返回值
    ListNode reversedHead = reverseList(head.next);
    // 下一个节点的后继节点修改为当前节点
    head.next.next = head;
    // 当前节点的后继节点修改为null
    head.next = null;

    return reversedHead;
}
```

该方法的时间复杂度为O(n)，其中n为链表的长度。空间复杂度为O(n)，因为线程栈的深度为n。