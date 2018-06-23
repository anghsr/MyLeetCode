# Z字形变换

##### 题目：

将字符串 `"PAYPALISHIRING"` 以Z字形排列成给定的行数：

```
P   A   H   N
A P L S I I G
Y   I   R
```

之后从左往右，逐行读取字符：`"PAHNAPLSIIGYIR"`

实现一个将字符串进行指定行数变换的函数:

```
string convert(string s, int numRows);
```

##### 示例1：

```
输入: s = "PAYPALISHIRING", numRows = 3
输出: "PAHNAPLSIIGYIR"
```

##### 示例2：

```
输入: s = "PAYPALISHIRING", numRows = 4
输出: "PINALSIGYAHRPI"
解释:

P     I    N
A   L S  I G
Y A   H R
P     I
```

##### 思路：

法1：

考虑按行来看，第一行的一个元素是字符串的第一个元素，后面的元素的位置是标记的元素在字符串上的位置加上2\*numRows-2。最后一行的元素同理可得。中间的行的元素分为两种情况，一种是当前元素位置加上numRows\*2-2-2\*行数，一种是当前元素位置加上2*行数，两种类型交替。

法2:

按列来考虑，只要从0->numRows-1和numRows-1->0循环，将s的元素一一放入再把numRows行的字符串拼接在一起就可以。

##### 解答（1）：

```python
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows==1:
            return s
        L = list(s)
        C = []
        for i in range(0,numRows):
            z = i
            while z<len(L):
                if i == 0:
                    C.append(L[z])
                    z = z + numRows*2-2
                elif i == numRows -1:
                    C.append(L[z])
                    z = z + numRows*2-2
                else:
                    C.append(L[z])
                    z = z + numRows*2-2-2*i
                    if z>=len(L):
                        break
                    C.append(L[z])
                    z = z + 2*i
        return "".join(C)
```

##### 解答（2）：

```python
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """    
        if numRows ==1 or numRows >= len(s):
            return s
        
        index, step = 0, 1
        l = [""] * numRows
        
        for item in s:
            l[index] += item
            if index == 0:                
                step = 1
            if index == numRows - 1:
                step = -1
            index += step
            
        return "".join(l)
```

