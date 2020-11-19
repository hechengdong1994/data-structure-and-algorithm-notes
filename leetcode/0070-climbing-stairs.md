# climbing-stairs

https://leetcode-cn.com/problems/climbing-stairs/

## 1 问题分析

由归纳法可知，该问题可以看做：若要走到n层，可以走到n-1层，再上一层；或走到n-2层，再上2层。而n-1和n-2又与上述描述相同，因此，该问题最终转化为Fibonacci数列问题，即f(n)=f(n-1)+f(n-2)。

## 2 暴力计算

```java
public int climbStairs(int n) {
    return n <= 2 ? n : climbStairs(n - 1) + climbStairs(n - 2);
}
```

通过递归树的方式计算该方法的时间复杂度。

|      |      |      |      | 5    |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|      |      | 4    |      |      |      | 3    |      |
|      | 3    |      | 2    |      | 2    |      | 1    |
| 2    | 1    |      |      |      |      |      |      |

由于最后一层为少量的1，2节点，因此该树的层级数可简单的看作n-2，每层节点数的递推公式为2^n，即该方法的时间复杂度为O(2^n)。

## 3 缓存优化

显然地，暴力计算的方法中，存在很多入参重复的计算。因此，对已计算出的结果进行缓存，减少不必要的重复计算。

```java
Map<Integer, Integer> cache = new HashMap<>();
public int climbStairs(int n) {
    if (n <= 2){
        return n;
    }
    if (cache.containsKey(n)){
        return cache.get(n);
    }

    int result = climbStairs(n - 1) + climbStairs(n - 2);
    cache.put(n, result);
    return result;
}
```

因为对n中的每个值分别进行了一次计算，因此该方法的时间复杂度为O(n)；但同时，空间复杂度也为O(n)。

## 4 动态规划（滚动数组）

```java
public int climbStairs(int n) {
    if (n <= 2) {
        return n;
    }
    // s1，s2分别用于保存已经计算过的n-2和n-1
    int temp, s1 = 1, s2 = 2;
    for (int i = 3; i <= n; i++) {
        temp = s1;
        s1 = s2;
        s2 = s1 + temp;
    }
    return s2;
}
```

该方法的时间复杂度依然为O(n)，而空间复杂度优化为O(1)。

### 4.1 代码优化

对1，2可以看做f(1) = 0 + 1，f(2) = f(1) + f(1)。因此，调整初始值，即可不对n<2做特殊判断。

```java
public int climbStairs(int n) {
    // s1，s2，s3分别表示n-2、n-1、n
    int s1 = 0, s2 = 0, s3 = 1;
    for (int i = 1; i <= n; i++) {
        s1 = s2;
        s2 = s3;
        s3 = s1 + s2;
    }
    return s3;
}
```

