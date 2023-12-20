# Merge K Sorted List

Status: Not started
Tags: Heaps
Created time: December 8, 2023 11:24 AM

[https://leetcode.com/problems/merge-k-sorted-lists/](https://leetcode.com/problems/merge-k-sorted-lists/)

```python
from dataclasses import dataclass, field
import heapq

@dataclass(order=True)
class Container:
    key: int
    node: 'ListNode' = field(compare=False)
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        q = []
        for i in lists:
            if i:
                heapq.heappush(q, Container(i.val, i))
        
        dummy = ListNode()
        current = dummy

        while q:
            smallest = heapq.heappop(q)
            current.next = smallest.node
            current = current.next
            if smallest.node.next:
                smallest.node = smallest.node.next
                smallest.key = smallest.node.val
                heapq.heappush(q, smallest)
        current.next = None
        return dummy.next
```