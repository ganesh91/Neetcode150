# Add Two Numbers

Status: Not started
Summary: The document provides a Python solution for the "Add Two Numbers" problem on LeetCode. The solution uses a singly-linked list to represent the numbers and adds them digit by digit, considering carry values. The solution is implemented in the addTwoNumbers method of the Solution class.
Tags: Linked List
Last edited time: November 23, 2023 4:00 PM

[https://leetcode.com/problems/add-two-numbers/description/](https://leetcode.com/problems/add-two-numbers/description/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        if not l2:
            return l1
        if not l1:
            return l2
        
        lptr = l1
        rptr = l2
        result = ListNode(-1)
        temp = result
        carry = 0

        while lptr or rptr or carry:
            new_node, carry = self.add(lptr, rptr, carry)
            temp.next = new_node
            temp = new_node
            if lptr:
                lptr = lptr.next
            if rptr:
                rptr = rptr.next
        
        return result.next

    

    def add(self, l1, l2, carry):
        total = carry
        if l1:
            total += l1.val
        if l2:
            total += l2.val
        carry = 0 if total <=9 else 1
        number = total % 10
        return ListNode(number), carry
```