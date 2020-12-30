# container-with-most-water

https://leetcode-cn.com/problems/container-with-most-water/

## 1 暴力求解

算法流程：双重循环，每两个数计算一次面积，保存面积最大的结果，即为最终结果。

```java
public int maxArea(int[] height) {
    int result = 0;
    // 内外层循环边界注意
    for (int i = 0; i < height.length - 1; i++) {
        for (int j = i + 1; j < height.length; j++) {
            // 计算面积
            int area = (j - i) * (height[i] > height[j] ? height[j] : height[i]);
            // 面积大小比较与替换
            if (area > result) {
                result = area;
            }
        }
    }
    return result;
}
```

该方法是最直观的，显然其时间复杂度为O(n^2)。

## 2 双指针

算法流程：

1. 双指针分别指向数组头尾两个元素
4. 左指针索引<右指针索引时进入循环
   1. 计算当前指针元素围成的面积并与目前最大的面积进行比较
   2. 比较左右指针元素的大小，移动元素值较小的指针，若两元素相等，任意移动一个

```java
public int maxArea(int[] height) {
    int i = 0;
    int j = height.length - 1;
    int result = 0;
    for (; i < j; ) {
        int area = (j - i) * (height[i] > height[j] ? height[j] : height[i]);
        if (area > result) {
            result = area;
        }
        if (height[i] > height[j]) {
            j--;
        } else {
            i++;
        }
    }
    return result;
}
```

该方法的时间复杂度为O(n)。
