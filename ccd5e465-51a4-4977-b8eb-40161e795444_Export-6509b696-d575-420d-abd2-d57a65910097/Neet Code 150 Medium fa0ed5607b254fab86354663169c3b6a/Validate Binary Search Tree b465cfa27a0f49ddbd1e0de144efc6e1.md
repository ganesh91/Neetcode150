# Validate Binary Search Tree

Status: Not started
Tags: DFS
Last edited time: November 25, 2023 8:12 PM

[https://leetcode.com/problems/validate-binary-search-tree/submission](https://leetcode.com/problems/validate-binary-search-tree/submissions/1106106246/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        return self.check(root, float('-inf'), float('inf'))
    
    def check(self, node, lower_bound, upper_bound):
        if not node:
            return True
        isBST = lower_bound < node.val < upper_bound
        left = self.check(node.left, lower_bound, node.val)
        right = self.check(node.right, node.val, upper_bound)
        return left and right and isBST
```