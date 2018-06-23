# 无重复字符的最长子串 

##### 题目：

给定一个字符串，找出不含有重复字符的**最长子串**的长度。 

##### 示例：

给定 `"abcabcbb"` ，没有重复字符的最长子串是 `"abc"` ，那么长度就是3。

给定 `"bbbbb"` ，最长的子串就是 `"b"` ，长度是1。

给定 `"pwwkew"` ，最长子串是 `"wke"` ，长度是3。请注意答案必须是一个**子串**，`"pwke"` 是 *子序列*  而不是子串。

##### 思路：

先将所给的字符串转换为列表，方便处理。然后创建一个临时列表，用于存放子串。遍历列表，如果字符不在临时列表中，就将字符放进列表中，并将计数器加1。如果字符在子串中，就先判断这个子串的长度是否比前一个子串长，如果是，把最长子串的长度设为该子串的长度。然后从重复的字符之后一个字符开始进行切片。获得不重复的子串部分。最后考虑全都不重复的情况，把最长子串长度设为计数器长度。

##### 解答：

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        L = list(s)
        Temp = []
        count = 0
        maxm = 0
        for l in L:
            if l not in Temp:
                Temp.append(l)
                count = count + 1
            else:
                if maxm<count:
                    maxm =  count
                Temp = Temp[Temp.index(l)+1:]
                Temp.append(l)
                count = len(Temp)
        if maxm < count:
            maxm = count
        return maxm
```

