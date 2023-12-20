# 606. Construct String from Binary Tree

Status: Not started
Tags: Recursion

[https://leetcode.com/problems/construct-string-from-binary-tree/](https://leetcode.com/problems/construct-string-from-binary-tree/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def tree2str(self, root: Optional[TreeNode]) -> str:
        if not root:
            return ()
        result_val = []
        self.construct(root, result_val)
        return "".join(result_val)
    
    def construct(self, node, result):
        result.append(str(node.val))
        if node.left:
            result.append('(')
            self.construct(node.left, result)
            result.append(')')
        if not node.left and node.right:
            result.append('()')
        if node.right:
            result.append('(')
            self.construct(node.right, result)
            result.append(')')
```