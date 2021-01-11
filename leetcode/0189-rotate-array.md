# rotate-array

https://leetcode-cn.com/problems/rotate-array/

## 1 循环移动

算法流程：

1. 循环k次，每次进行一次右移
   1. 临时存放最右的一个元素
   2. 将前面的元素向后移一位
   3. 将原来最右的元素放在第一个位置

```java
public void rotate(int[] nums, int k) {
    // 循环k次，每次向右旋转一次
    for (int i = 0; i < k; i++) {
        // 临时保存数组最后一个元素
        int temp = nums[nums.length-1];
        // 前面的length-1个元素后移一位
        System.arraycopy(nums, 0, nums, 1, nums.length-1);
        // 将原数组最后一个元素放在第一位
        nums[0] = temp;
        // 即完成一次旋转
    }
}
```

该方法的时间复杂度为O(n*O(arraycopy))，空间复杂度为O(1)。这里借助了java内置的数组复制函数，但依然效率较低。

### 1.1 操作次数优化

优化内容：

1. 对旋转次数k进行修正，对数组长度取余，因为旋转length次又回到了原样
2. 直接保存数组的后k个元素，而不是循环k次，每次旋转一个元素

```java
public void rotate(int[] nums, int k) {
    k %= nums.length;
    if (k == 0) {
        return;
    }
    int[] temp = new int[k];
    System.arraycopy(nums, nums.length - k, temp, 0, k);
    System.arraycopy(nums, 0, nums, k, nums.length - k);
    System.arraycopy(temp, 0, nums, 0, k);
}
```

经过该优化后，依然借助内置arraycope函数，但因为没有进行多次循环，因此运行的速率得到明显提升。在此算法下，时间复杂度降低为O(arraycopy(n)+arraycopy(k))，但空间复杂度提升到O(k)。

## 2 环状替换

算法流程：

1. 对k进行取余修正
2. 从数组的第一个元素开始，进入外循环，直到操作次数与数组元素个数相同，退出循环
   1. 计算该元素经过旋转后的索引
   2. 临时保存新索引的元素
   3. 将该元素放到新位置，操作次数+1
   4. 继续对新位置的元素，重复上述操作，直到计算出的新索引与初始索引相同，退出内循环

```java
public void rotate(int[] nums, int k) {
    k %= nums.length;
    if (k == 0) {
        return;
    }
    int count = 0;
    // 从数组的第一个元素开始，直到操作次数与数组元素个数相同
    for (int start = 0; count < nums.length; start++) {
        // 内循环从当前起始元素开始
        int i = start;
        int current = nums[i];
        do {
            // 计算旋转k次后的索引
            i = (i + k) % nums.length;
            // 保存目标索引上的元素
            int temp = current;
            // 当前处理元素移动
            current = nums[i];
            nums[i] = temp;
            // 操作次数+1
            count++;
            // 当前元素索引与初始索引相同时，结束内循环
        } while (i != start);
    }
}
```

该方法中的对count==nums.length即完成所有交换的判断，其依据在于，每一次的有效交换，都有一个元素被放到了经过k次旋转后最终正确的位置上，因此，只需要进行nums.length次有效交换，就表示所有的元素都已经在最终正确的位置上了。对每次的内循环，当索引与其实索引不同时的交换均为有效交换。

该方法的时间复杂度为O(n)，因为所有的元素仅遍历了一次；空间复杂度为O(1)，因为仅额外适用了固定大小的临时变量。

## 3 数组翻转

算法流程

1. 翻转原数组
2. 翻转0到k-1的元素
3. 翻转k到length-1的元素

```java
public void rotate(int[] nums, int k) {
    k %= nums.length;
    if (k == 0) {
        return;
    }
    // 翻转原数组
    revert(nums, 0, nums.length - 1);
    // 翻转0到k-1的元素
    revert(nums, 0, k - 1);
    // 翻转看到length-1的元素
    revert(nums, k, nums.length - 1);
}

private void revert(int[] nums, int left, int right) {
    for (; left < right; left++, right--) {
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
}
```

该方法的时间复杂度为O(2n)，因为遍历了两次数组；空间复杂度为O(1)，因为仅额外适用了固定大小的临时变量。