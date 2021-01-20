# linked-list-cycle-ii

https://leetcode-cn.com/problems/linked-list-cycle-ii/

基于

[141.linked-list-cycle]: 0141-linked-list-cycle.md

## 1 额外空间存储

1. 算法流程：

   1. 初始化：声明一个额外的HashSet保存遍历过的节点
   2. 从head开始循环遍历元素。若HashSet中包含当前节点，则表示存在循环，返回true；否则，将当前节点存入HashSet中。
   3. 遍历结束，则表示不存在循环，返回false。

```java
public ListNode detectCycle(ListNode head) {
    // 声明一个额外的空间保存遍历过的节点
    Set<ListNode> seenNodes = new HashSet<>();
    // 遍历元素
    for (; head != null; head = head.next) {
        // 集合中包含当前节点，表示首次遇到了环中的元素，即首个元素
        if (seenNodes.contains(head)) {
            return head;
        }
        // 将当前节点存入集合中
        seenNodes.add(head);
    }
    // 遍历结束，则表示当前链表中不存在环
    return null;
}
```

该方法的时间复杂度为O(n)。空间复杂度为O(n)，因为声明了额外的集合存放已遍历元素。

## 2 快慢指针

算法思想：如果链表中存在环，则快慢指针进入环中后，最终一定会在某个元素上相遇。当快慢指针相遇时，他们走过的节点数的关系为快指针总路程=慢指针总路程+n环长。进一步将整个链表分为环之前的元素个数a，快慢指针相遇时距离环首个节点的元素个数b，环中其他元素个数c（即环长-b）。则快指针的总路程为为a+b+n（b+c）。又由于快指针总路程=2慢指针路程，即，a+b+n（b+c）=2（a+b）。整理得到a=c+（n-1）（b+c）。因此，当快慢指针相遇时，再额外使用一个指针result从链表头部开始，它和慢指针每次向后移动一个位置。最终，它们会在入环点相遇。

算法流程：

1. 初始化：声明快指针指向head
2. 当快指针及其下一节点不为null时，进入循环
   1. 慢指针后移一位
   2. 快指针后移两位
   3. 若快慢指针指向相同元素，则链表中存在环，跳出循环
   4. 声明结果指针result指向head，慢指针与结果指针每次后移一位，直到相遇，则result指针指向环首个元素
3. 循环正常结束，表示快指针走到了链表尾部，即链表中不存在环，返回null

```java
public ListNode detectCycle(ListNode head) {
    // 初始化快慢指针指向第一个元素
    ListNode slow = head;
    ListNode fast = head;
    // 初始化bool表示是否存在环
    boolean hasCycle = false;
    // 当快指针未走到尾部时，进入循环
    while (fast != null && fast.next != null) {
        // 慢指针后移一位
        slow = slow.next;
        // 快指针后移两位
        fast = fast.next.next;
        // 若快慢指针指向相同元素，表示链表中存在环
        if (slow == fast) {
            hasCycle = true;
            break;
        }
    }
    // 链表中不存在环，直接返回
    if (!hasCycle) {
        return null;
    }

    // 声明结果指针指向head
    ListNode result = head;
    while (result != slow) {
        // 慢指针后移一位
        slow = slow.next;
        // 结果指针后移一位
        result = result.next;
    }
    // 返回结果指针
    return result;
}
```

该方法的时间复杂度为O(n)。空间复杂度为O(1)，因为只额外声明了快慢指针和结果指针。