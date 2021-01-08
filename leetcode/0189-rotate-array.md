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

