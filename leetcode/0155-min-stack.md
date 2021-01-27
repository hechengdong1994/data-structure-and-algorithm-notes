# min-stack

https://leetcode-cn.com/problems/min-stack/

## 1 双栈

算法思想：借助java中内置的栈数据结构进行。额外使用一个栈记录历史最小值。

```java
class MinStack {

    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    /**
     * initialize your data structure here.
     */
    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int x) {
        stack.push(x);
        // 最小值处理：如果当前值<=最小值栈的栈顶元素，则将当前值入最小值栈。
        // 需要注意此处判断规则为<=，因为可能连续插入多个相同值
        if (minStack.empty() || minStack.peek() >= x) {
            minStack.push(x);
        }
    }

    public void pop() {
        if (stack.empty()) {
            return;
        }
        int x = stack.pop();
        // 最小值处理：如果当前值=最小值，则最小值栈需要进行出栈处理
        if (x == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

## 2 单栈

算法思想：借助java中内置的栈数据结构进行。但不额外使用一个栈记录历史最小值。而是使用一个额外的变量记录最小值。为了解决最小值的变化问题，对入栈操作进行特殊处理。

```java
class MinStack {

    private Stack<Integer> stack;
    // 最小值初始化为int类型的最大值
    private int min = Integer.MAX_VALUE;

    /**
     * initialize your data structure here.
     */
    public MinStack() {
        stack = new Stack<>();
    }

    public void push(int x) {
        // 先进行最小值处理：若当前值<=最小值，则将当前最小值入栈，再更新最小值
        if (min >= x) {
            stack.push(min);
            min = x;
        }
        // 再将元素入栈
        stack.push(x);
    }

    public void pop() {
        // 出栈时先将元素出栈
        // 再进行最小值处理：若当前出栈值为最小值，则再次出栈，并设置为最小值
        if (min == stack.pop()) {
            min = stack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return min;
    }
}
```

## 3 自定义节点结构

算法思想：由于栈基于链表来实现，因此可以自己实现链表的方式来实现栈。定义栈中的节点结构，增加一个变量保存目前已有的栈元素中最小的值。

```java
class MinStack {

    // 自定义链表节点，包含当前值；目前为止的最小值；下一元素指针
    class Node {
        int value;
        Node next;
        int min;
    }

    private Node top;

    /**
     * initialize your data structure here.
     */
    public MinStack() {
        top = null;
    }

    public void push(int x) {
        Node node = new Node();
        node.value = x;
        node.next = top;
        node.min = top == null ? x : (top.min >= x ? x : top.min);
        top = node;
    }

    public void pop() {
        top = top.next;
    }

    public int top() {
        return top.value;
    }

    public int getMin() {
        return top.min;
    }
}
```

该方法的空间使用相对多一些。