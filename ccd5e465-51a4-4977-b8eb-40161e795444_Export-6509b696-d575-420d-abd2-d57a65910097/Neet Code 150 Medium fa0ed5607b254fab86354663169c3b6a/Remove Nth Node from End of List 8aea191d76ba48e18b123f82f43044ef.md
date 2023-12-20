# Remove Nth Node from End of List

Status: Not started
Tags: Linked List
Last edited time: November 27, 2023 2:36 PM

[https://leetcode.com/problems/remove-nth-node-from-end-of-list/](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        if not head:
            return head
        
        dummy = ListNode()
        dummy.next = head

        start = 0
        fast = dummy
        slow = dummy
        while start < n and fast:
            fast = fast.next
            start += 1
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next
        
        slow.next = slow.next.next
        return dummy.next
```