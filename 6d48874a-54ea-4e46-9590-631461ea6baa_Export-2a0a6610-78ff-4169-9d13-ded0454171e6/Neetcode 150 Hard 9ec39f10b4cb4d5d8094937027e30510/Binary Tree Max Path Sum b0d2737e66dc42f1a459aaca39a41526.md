# Binary Tree Max Path Sum

Status: Not started
Tags: Trees
Created time: December 19, 2023 3:17 PM

[https://leetcode.com/problems/binary-tree-maximum-path-sum/](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        self.count(root)
        return self.tree_max(root)
    
    def count(self, node):
        if not node:
            return float('-inf')
        left = self.count(node.left)
        right = self.count(node.right)
        currMax = max(node.val, node.val+left, node.val+right, node.val+left+right)
        node.mx = currMax
        return max(node.val, node.val+left, node.val+right)
    
    def tree_max(self, node):
        if not node:
            return float('-inf')
        return max(node.mx, self.tree_max(node.left), self.tree_max(node.right))
```