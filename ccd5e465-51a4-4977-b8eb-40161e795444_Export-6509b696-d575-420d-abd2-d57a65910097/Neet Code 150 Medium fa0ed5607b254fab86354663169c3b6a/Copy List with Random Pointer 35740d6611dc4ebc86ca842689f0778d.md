# Copy List with Random Pointer

Status: Not started
Summary: The "Copy List with Random Pointer" problem involves creating a deep copy of a linked list with random pointers. The solution suggests iterating through the list twice, first to copy the main list and create a lookup for the new nodes, and then to fill in the random pointers using the lookup. The provided Python code implements this solution.
Tags: Linked List
Last edited time: November 23, 2023 1:48 PM

[https://leetcode.com/problems/copy-list-with-random-pointer/editorial/](https://leetcode.com/problems/copy-list-with-random-pointer/editorial/)

Idea: 

- Iterate once and copy the main list
- Create a lookup for the newly committed node
- Iterate once more and fill in the random

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return head
        
        original_head = head
        dummy_head = Node(-1)
        dummy = dummy_head
        lookup = {}
        counter = 0
        while head:
            new_node = Node(head.val)
            head.counter = counter
            lookup[counter] = new_node
            dummy.next = new_node
            dummy = dummy.next
            head = head.next
            counter += 1
        
        head = original_head
        dummy = dummy_head.next
        while head:
            if head.random:
                index = head.random.counter
                dummy.random = lookup[index]
            head = head.next
            dummy = dummy.next
        
        return dummy_head.next
```