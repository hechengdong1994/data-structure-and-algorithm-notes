# linked-list-cycle

https://leetcode-cn.com/problems/linked-list-cycle/

## 1 额外空间存储

算法流程：

1. 初始化：声明一个额外的HashSet保存遍历过的节点
2. 从head开始循环遍历元素。若HashSet中包含当前节点，则表示存在循环，返回true；否则，将当前节点存入HashSet中。
3. 遍历结束，则表示不存在循环，返回false。

```java
public boolean hasCycle(ListNode head) {
    // 声明一个额外的空间保存遍历过的节点
    Set<ListNode> seenNodes = new HashSet<>();
    // 遍历元素
    for (; head != null; head = head.next) {
        // 集合中包含当前节点，表示存在环
        if (seenNodes.contains(head)) {
            return true;
        }
        // 将当前节点存入集合中
        seenNodes.add(head);
    }
    // 遍历结束，则表示当前链表中不存在环
    return false;
}
```

该方法的时间复杂度为O(n)。空间复杂度为O(n)，因为声明了额外的集合存放已遍历元素。

## 2 快慢指针

算法思想：使用快慢指针在链表中遍历元素。如果不存在环，则快指针会首先走到链表的尾部；如果链表中存在环，则快指针先进入环中，慢指针后进入环中，并且最终一定会在某个元素上相遇。

算法流程：

1. 初始化：声明快指针指向head
2. 当快指针及其下一节点不为null时，进入循环
   1. 慢指针后移一位
   2. 快指针后移两位
   3. 若快慢指针指向相同元素，则链表中存在环
3. 循环结束，表示快指针走到了链表尾部，即链表中不存在环

```java
public boolean hasCycle(ListNode head) {
    // 初始化快慢指针指向第一个元素
    ListNode slow = head;
    ListNode fast = head;
    // 当快指针未走到尾部时，进入循环
    while (fast != null && fast.next != null) {
        // 慢指针后移一位
        slow = slow.next;
        // 快指针后移两位
        fast = fast.next.next;
        // 若快慢指针指向相同元素，表示链表中存在环
        if (slow == fast) {
            return true;
        }
    }
    // 退出循环，表示快指针走到了链表尾部，说明链表中不存在环
    return false;
}
```

需要注意，该实现中先进行快慢指针移动再进行指针指向元素比较，是为了避免在一开始时快慢指针都指向第一个元素时的判断。

该方法的时间复杂度为O(n)。空间复杂度为O(1)，因为只额外声明了快慢指针。