# remove-duplicates-from-sorted-array

https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/

## 1 快慢指针

算法流程：

1. 快慢指针起始指向数组第一个元素，数组元素个数结果初始值为1（额外判断数组中没有元素的情况）
4. 快指针遍历数组中所有元素
   1. 若快慢指针指向的元素不同，则慢指针后移一位，然后交换快慢指针指向的元素，同时数组元素个数+1
   2. 若快慢指针指向的元素相同，则不操作
3. 返回数组元素个数结果

```java
public int removeDuplicates(int[] nums) {
    // 对数组中没有数据的情况进行特殊判断
    if (nums.length == 0) {
        return 0;
    }
    // 返回值的数组元素个数至少为1
    int result = 1;
    for (int i = 0, j = 0; j < nums.length; j++) {
        if (nums[i] != nums[j]) {
            // 慢指针后移
            i++;
            // 数据交换
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
            // 数组元素个数+1
            result++;
        }
    }
    return result;
}
```

该方法的时间复杂度为O(n)，空间复杂度为O(1)。

### 1.1 操作次数优化

```java
public int removeDuplicates(int[] nums) {
    // 对数组中没有数据的情况进行特殊判断
    if (nums.length == 0) {
        return 0;
    }
    // 慢指针
    int i = 0;
    for (int j = 0; j < nums.length; j++) {
        if (nums[i] != nums[j]) {
            i++;
            // 直接进行数据赋值，因题干中只需要不重复的数据，因此可以不必做数据交换
            nums[i] = nums[j];
        }
    }
    // 慢指针的索引值+1即为新数组的元素个数
    return i + 1;
}
```

对一些不必要的操作进行了优化。结果满足题干要求。但从leetcode给出的性能结果来看，没有很大的提升。

