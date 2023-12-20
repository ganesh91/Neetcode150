# Binary Tree Level Order Traversal

Status: Not started
Tags: BFS
Last edited time: November 25, 2023 7:35 PM

[https://leetcode.com/problems/binary-tree-level-order-traversal/](https://leetcode.com/problems/binary-tree-level-order-traversal/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return root
        q = deque([root])
        levels = []
        while q:
            count = len(q)
            current = []
            while count:
                item = q.popleft()
                current.append(item.val)
                if item.left:
                    q.append(item.left)
                if item.right:
                    q.append(item.right)
                count -= 1
            levels.append(current)
        return levels
```