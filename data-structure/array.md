# 数组

## 1 简介

数组是一维的、线性的数据结构，使用一段连续的内存空间来存储一组类型相同的数据。通过偏移量（或称索引/下标）标识每个数据的位置，偏移量从0开始。

## 2 操作及时间复杂度

### 随机访问

由于数组使用连续内存空间的存储方式，根据数组下标访问数据时，只需要常数级的计算即可得到元素的实际地址。因此数组的随机访问操作的时间复杂度为O(1)。

常数级的数据访问速度也是数组这一数据结构的优势。

### 插入

将数据插入数组中的非尾部位置，需要将该位置的后续元素全部后移一位。因此数组的数据插入时间复杂度为O(n)。

若该次数据插入引起了数据扩容，则还需要进行一次时间复杂度为O(n)的数据复制操作。

根据平均分配原则，数组的数据插入操作的平均时间复杂度为O(n)。

### 修改

修改数组中指定下标的数据时，需要先通过随机访问方式查找到该数据，再进行数据替换。因此数组的数据修改时间复杂度为O(1+1)，即O(1)。

### 删除

从数组中删除数据，为了保证数据的连续性，需要将后续的元素全部前移一位。因此数组的数据删除时间复杂度为O(1+n)，即O(n)。

## 3 相关问题

[11.container-with-most-water](../leetcode/0011-container-with-most-water.md)

[283.move-zeroes](../leetcode/0283-move-zeroes.md)

[70.climbing-stairs](../leetcode/0070-climbing-stairs.md)

[15.3sum](../leetcode/0015-3sum.md)

[1.two-sum](../leetcode/0001-two-sum.md)

[26.remove-duplicates-from-sorted-array](../leetcode/0026-remove-duplicates-from-sorted-array.md)

[88.merge-sorted-array](../leetcode/0088-merge-sorted-array.md)

[66.plus-one](../leetcode/0066-plus-one.md)

[189.rotate-array](../leetcode/0189-rotate-array.md)

