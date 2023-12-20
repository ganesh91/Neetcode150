# Reverse Nodes in K-Group

Status: Not started
Tags: Linked List
Created time: December 8, 2023 1:42 PM

[https://leetcode.com/problems/reverse-nodes-in-k-group](https://leetcode.com/problems/reverse-nodes-in-k-group)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        size = 0
        tmp = head
        while tmp:
            tmp = tmp.next
            size += 1
        
        if size < k or k == 1:
            return head
        
        n_groups = size // k
        
        root = ListNode()
        prev, current, last = None, head, None

        while n_groups:
            c_prev, c_current, c_last = self.reverse(current, k)
            if not root.next:
                root.next = c_prev
            if last:
                last.next = c_prev
            current, last = c_current, c_last
            n_groups -= 1
        
        if current:
            last.next = current
            
        return root.next

    
    def reverse(self, node, k):
        last_node = node
        prev, current = None, node
        while current and k:
            tmp = current.next
            current.next = prev
            prev = current
            current = tmp
            k -= 1
        return (prev, current, last_node)
```