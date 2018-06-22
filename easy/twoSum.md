# 两数之和

给定一个整数数组和一个目标值，找出数组中和为目标值的**两个**数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**示例：**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

**思路：**

首先，把数组nums放到一个字典dic中，数组元素作为键，对应的索引作为值。然后遍历数组nums，用目标值减去数组中的元素nums[count]得到一个值x，然后判断这个值x是否是字典的键，如果是，并且不是本身的元素，返回数组元素nums[count]的索引和键为x的值组成的列表[count,dic[x]]。

**解答（使用Python）：**

```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        dic = {}
        count = 0
        for i in nums:
            dic[i] = count
            count = count + 1
        count = 0
        for temp in nums:
            x = target - temp
            if (x in dic) and dic[x]!= count:
                return [count,dic[x]]
            count = count + 1
```

