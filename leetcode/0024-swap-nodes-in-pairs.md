# swap-nodes-in-pairs

https://leetcode-cn.com/problems/swap-nodes-in-pairs/

类比

[206.reverse-linked-list]: 0206-reverse-linked-list.md

## 1 迭代

算法流程：

1. 初始化：声明哑结点，指向head元素
2. 当前元素的后两个元素不为空时，遍历链表
   1. 临时保存temp=当前元素的next元素
   2. 交换后续两个元素
   3. 更改当前引用后移两个元素

```java
public ListNode swapPairs(ListNode head) {
    // 声明哑结点，指向head元素
    head = new ListNode(0, head);
    // 声明结果变量，指向头元素，用于结果返回
    ListNode result = head;
    // 当后续两个元素都有值时，即需要进行替换，进入循环
    while (head.next != null && head.next.next != null) {
        // 临时元素
        ListNode temp = head.next;
        // 后续两个元素的交换
        head.next = head.next.next;
        temp.next = head.next.next;
        head.next.next = temp;
        // 指针后移
        head = head.next.next;

    }
    // 返回结果
    return result.next;
}
```

该方法的时间复杂度为O(n)，其中n为链表的长度。空间复杂度为O(1)。

## 2 递归

```java
public ListNode swapPairs(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    // swapedHead指向的是所有经过交换后的链表的第一个元素
    ListNode swapedHead = swapPairs(head.next.next);

    // 最终的返回值为待交换的第二个元素
    ListNode result = head.next;
    // 两元素交换
    head.next.next = head;
    head.next = swapedHead;
    return result;
}
```

该方法的时间复杂度为O(n)，其中n为链表的长度。空间复杂度为O(n)，因为线程栈的深度为n。