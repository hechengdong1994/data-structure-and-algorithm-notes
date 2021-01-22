# reverse-nodes-in-k-group

https://leetcode-cn.com/problems/reverse-nodes-in-k-group/

扩展自

[206.reverse-linked-list](0206-reverse-linked-list.md)
[24.swap-nodes-in-pairs](0024-swap-nodes-in-pairs.md)

## 1 迭代

算法流程：循环链表，每k个元素进行一个翻转

```java
public ListNode reverseKGroup(ListNode head, int k) {
    // 哑结点
    head = new ListNode(0, head);
    ListNode preResult = head;
    // 每k个一组进行一次翻转
    while (true) {
        // 保存第一个节点，翻转后该节点为最后一个节点，需要修改后继节点
        ListNode firstOfK = head.next;
        // 找到下一组k节点
        ListNode tail = head;
        for (int i = 1; i <= k; i++) {
            if (tail.next == null) {
                return preResult.next;
            }
            tail = tail.next;
        }
        // 暂存该组的下一个节点，翻转后需要连接
        ListNode tailNext = tail.next;
        // k个元素翻转，返回翻转后的第一个节点
        ListNode reversed = reverseList(head.next, tail.next);
        // 翻转后连接到原链表上
        head.next = reversed;
        firstOfK.next = tailNext;
        // 后移head
        head = firstOfK;
    }
}

public ListNode reverseList(ListNode head, ListNode tail) {
    ListNode current = null;
    while (head != null && head != tail) {
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

该方法的时间复杂度为O(n)。空间复杂度为O(1)。
