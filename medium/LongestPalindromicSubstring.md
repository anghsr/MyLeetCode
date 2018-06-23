# 最长回文子串

##### 题目：

给定一个字符串 **s**，找到 **s** 中最长的回文子串。你可以假设 **s** 的最大长度为1000。 

##### 示例1：

```
输入: "babad"
输出: "bab"
注意: "aba"也是一个有效答案。
```

##### 示例2：

```
输入: "cbbd"
输出: "bb"
```

##### 算法：马拉车算法（Manacher）

时间复杂度：O（n）

首先在每个字符前后都添加分隔符#，然后在字符串的前后分别添加^和$，并把处理后的字符串记为t。这样处理之后可以把奇偶长度的回文串都用同一种方法处理。

设置一个列表p作为以每个位置为中心的回文串长度，c为中心点，d为最大值。然后遍历t，求出p，最后得出t上的最长回文串的中心i和半径k，然后对s进行切片，得出结果。

##### 解答（Python）：

```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        assert '$' not in s and '^' not in s and '#' not in s
        if s =='':
            return s
        t = "^#" + "#".join(s) + "#$"
        c = 0
        d = 0
        p = [0]*len(t)
        for i in range(1,len(t) - 1):
            mirror=2*c-i
            p[i] = max(0,min(d-i,p[mirror]))
            
            while t[i+1+p[i]]==t[i-1-p[i]]:
                p[i] += 1
            
            if i+p[i] >d:
                c=i
                d=i+p[i]
        (k,i) = max((p[i],i) for i in range(1,len(t) - 1))
        z = s[(i-k)//2:(i+k)//2]
        return z
```

