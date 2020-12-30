# two-sum

https://leetcode-cn.com/problems/two-sum/

## 1 哈希表

算法流程：

1. 额外声明一个哈希表存储<已遍历的整数，该整数的索引>
2. 遍历数组元素
   1. 根据当前元素计算要满足target所需要的整数值，即need=target-当前元素
   2. 查询哈希表，若该结果已存在，则找到结果，直接返回；若不存在，则将当前元素及其索引存入哈希表中，供后续元素的处理进行查询。
3. 若遍历完所有元素依然无结果，返回空数组

```java
public int[] twoSum(int[] nums, int target) {
    // 声明额外的哈希表用于存储数组的<元素，索引>
    Map<Integer, Integer> targetMap = new HashMap<>();
    // 遍历数组元素
    for (int i = 0; i < nums.length; i++) {
        // 计算要达到目标值target所需的整数
        int need = target - nums[i];
        // 在哈希表中查找该元素
        if (targetMap.get(need) != null) {
            // 查询到该元素，则返回由这两个元素的索引构成的数组
            return new int[]{targetMap.get(need), i};
        } else {
            // 未查询到该元素，则将当前元素及其索引存入哈希表中，供后续元素的处理查询
            targetMap.put(nums[i], i);
        }
    }
    // 若遍历完所有元素依然无结果，返回空数组
    return new int[2];
}
```

该方法的时间复杂度为O(n)，空间复杂度为O(n)。
