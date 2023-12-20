# Count Good Nodes in a Binary Tree

Status: Not started
Tags: DFS
Last edited time: November 25, 2023 8:06 PM

[https://leetcode.com/problems/count-good-nodes-in-binary-tree/submissions/](https://leetcode.com/problems/count-good-nodes-in-binary-tree/submissions/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        return self.calculate(root, float('-inf'))
    
    def calculate(self, root, max_so_far):
        if not root:
            return 0
        left = self.calculate(root.left,max(max_so_far, root.val))
        right = self.calculate(root.right, max(max_so_far, root.val))
        current = 1 if root.val >= max_so_far else 0
        return left+right+current
```