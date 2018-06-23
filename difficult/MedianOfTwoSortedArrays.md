# 两个排序数组的中位数

##### 题目：

给定两个大小为 m 和 n 的有序数组 **nums1** 和 **nums2** 。

请找出这两个有序数组的中位数。要求算法的时间复杂度为 O(log (m+n)) 。

##### 示例1：

```
nums1 = [1, 3]
nums2 = [2]

中位数是 2.0
```

##### 示例2：

```
nums1 = [1, 2]
nums2 = [3, 4]

中位数是 (2 + 3)/2 = 2.5
```

##### 思路：

首先将第二个列表接到第一个列表之后，然后进行排序。（也可以遍历第一个列表，将第二个列表的元素按大小直接插入）然后得到中位数所在的索引。最后算出中位数。

##### 解答（Python）：

```python
class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        nums1.extend(nums2)
        nums1.sort()
        mid = len(nums1)/2
        midx = int(mid)
        if mid==midx:
            z = (nums1[midx-1]+nums1[midx])/2
        else:
            z = nums1[midx]
        return z
```

