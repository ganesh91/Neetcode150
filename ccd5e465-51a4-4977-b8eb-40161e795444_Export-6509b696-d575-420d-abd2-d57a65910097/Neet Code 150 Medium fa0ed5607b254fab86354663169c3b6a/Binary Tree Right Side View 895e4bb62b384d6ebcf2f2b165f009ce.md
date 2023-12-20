# Binary Tree Right Side View

Status: Not started
Tags: BFS, DFS
Last edited time: November 25, 2023 8:24 PM

[https://leetcode.com/problems/binary-tree-right-side-view/submissions/](https://leetcode.com/problems/binary-tree-right-side-view/submissions/)

BFS Version:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return root
        result = []
        q = deque([root])
        while q:
            size = len(q)
            while size:
                item = q.popleft()
                if size == 1:
                    result.append(item.val)
                if item.left:
                    q.append(item.left)
                if item.right:
                    q.append(item.right)
                size -= 1
        return result
```

DFS Version:

```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return root
        result = []
        levels_seen = set([])
        self.traverse(root, 0, levels_seen, result)
        return result
    
    def traverse(self, node, level, levels_seen, result):
        if level not in levels_seen:
            levels_seen.add(level)
            result.append(node.val)
        if node.right:
            self.traverse(node.right, level+1, levels_seen, result)
        if node.left:
            self.traverse(node.left, level+1, levels_seen, result)
```