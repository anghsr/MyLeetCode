# 字符串转整数（atoi）

##### 题目：

实现 `atoi`，将字符串转为整数。

在找到第一个非空字符之前，需要移除掉字符串中的空格字符。如果第一个非空字符是正号或负号，选取该符号，并将其与后面尽可能多的连续的数字组合起来，这部分字符即为整数的值。如果第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

字符串可以在形成整数的字符后面包括多余的字符，这些字符可以被忽略，它们对于函数没有影响。

当字符串中的第一个非空字符序列不是个有效的整数；或字符串为空；或字符串仅包含空白字符时，则不进行转换。

若函数不能执行有效的转换，返回 0。

**说明：**

假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−2^31,  2^31 − 1]。如果数值超过可表示的范围，则返回  INT_MAX (2^31 − 1) 或 INT_MIN (−2^31) 。

**示例 1:**

```
输入: "42"
输出: 42
```

**示例 2:**

```
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
```

**示例 3:**

```
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
```

**示例 4:**

```
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
```

**示例 5:**

```
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

##### 思路：

首先先把位置移到第一个非空字符，如果是-+数字之外的字符直接返回0，然后判断一下如果是+-符号，是否只是单个符号，是的话返回0，将字符串中的数字提取到列表num中，并把num转换为整数，如果溢出，返回最大（小）值，否则返回转换后的整数。

##### 解答：

```python
class Solution:
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        temp = list(str)
        flag = 0
        po = 1
        for t in temp:
            t = ord(t)
            if t==32:
                continue
            elif t>47 and t<58:
                flag = temp.index(chr(t))
                break
            elif t == 43 or t == 45:
                flag = temp.index(chr(t))
                temp.remove(chr(t))
                if t == 45:
                    po = -1
                break
            else:
                return 0
        if len(str)==0:
            return 0
        num = []
        while flag<len(temp):
            z = ord(temp[flag])
            if z>47 and z<58:
                num.append(chr(z))
            else:
                break
            flag += 1
        c = "".join(num)
        if c == "":
            return 0
        x = int(c)*po
        if x>2**31-1:
            return 2**31-1
        elif x<-2**31:
            return -2**31
        return x
```
