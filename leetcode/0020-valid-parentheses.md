# valid-parentheses

https://leetcode-cn.com/problems/valid-parentheses/

## 1 栈

算法流程：

1. 遍历字符串
   1. 如果是左括号，则将其入栈
   2. 如果是右括号，
      1. 当前栈为空，则直接返回false
      2. 弹出栈顶元素进行配对比较，不匹配则返回false，否则继续遍历
2. 遍历结束，若栈为空，则校验成功，反之校验失败。

```java
public boolean isValid(String s) {
    // 左右括号关系声明
    Map<Character, Character> valid = new HashMap<>(3);
    valid.put('(', ')');
    valid.put('[', ']');
    valid.put('{', '}');
    Stack<Character> stack = new Stack<>();
    for (int i = 0; i < s.length(); i++) {
        if (valid.keySet().contains(s.charAt(i))) {
            // 左括号入栈
            stack.push(s.charAt(i));
        } else {
            // 右括号则判断栈空并出栈匹配
            if (stack.empty() || s.charAt(i) != valid.get(stack.pop())) {
                return false;
            }
        }
    }
    return stack.empty();
}
```

该方法的时间复杂度为O(n+m)。空间复杂度为O(m)。其中，n为字符串长度，m为左右括号数量。

### 1.1 空间及操作次数优化

优化方案：

1. 不引入额外的哈希表数据结构
2. 对于左括号元素，将对应的右括号进行入栈；对于右括号，直接出栈并比较

```java
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();
    char c;
    for (int i = 0; i < s.length(); i++) {
        c = s.charAt(i);
        // 左括号，将对应的右括号入栈
        if (c == '(') {
            stack.push(')');
        } else if (c == '[') {
            stack.push(']');
        } else if (c == '{') {
            stack.push('}');
        } else if (stack.empty() || c != stack.pop()) {
            // 右括号，栈判空及出栈匹配
            return false;
        }
    }
    return stack.empty();
}
```

优化后，时间复杂度不变，但实际执行时间有减少。空间复杂度下降为O(1)。