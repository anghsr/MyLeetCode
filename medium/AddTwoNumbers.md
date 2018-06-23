# 两数相加

#### 题目：

给定两个**非空**链表来表示两个非负整数。位数按照**逆序**方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

##### 示例：

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

##### 思路：

最主要的是遍历两个链表，并将对应位置的数相加，存入新的链表的同一位置，要注意的是相加后的数可能大于9，所以可以设置一个标志变量carry，用来记录向前进位。这里用到的一个小技巧是和所用的链表是带有头结点的，这样可以用另一个变量进行循环，最后返回头结点的下一个结点就可以。

##### 解答（Python）：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        head = ListNode(0)
        p = l1
        q = l2
        curr = head
        carry = 0
        while p!=None or q!=None:
            if p!=None:
                x=p.val
            else:
                x=0
            if q!=None:
                y=q.val
            else:
                y=0
            sum = carry+x+y
            carry=int(sum/10)
            curr.next = ListNode(sum%10)
            curr = curr.next
            if p!=None:
                p=p.next
            if q!=None:
                q=q.next
        if carry >0:
            curr.next = ListNode(carry)
        return head.next
```

但这样写的执行用时为：180ms。并不十分理想。

执行时间为104ms的写法：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        p = l1
        q = l2
        t = None
        c = 0
        while p and q:
            p.val = p.val + q.val + c
            c = p.val // 10
            p.val = p.val%10
            t = p
            p = p.next
            q = q.next
        while p:
            p.val = p.val + c
            c = p.val //10
            p.val = p.val%10
            t = p
            p = p.next
        p = t
        p.next = q
        p = p.next
        while p:
            p.val = p.val + c
            c = p.val //10
            p.val = p.val%10
            t = p
            p = p.next
        if c == 1:
            p = t
            x = ListNode(1)
            p.next = x
        return l1
```

