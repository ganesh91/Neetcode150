# 94. Binary Tree Inorder Traversal

Status: Not started
Tags: Recursion, Stack

[https://leetcode.com/problems/binary-tree-inorder-traversal/](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Version 1:

- Recursive approach

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        collector = []
        self.collect(root, collector)
        return collector
    
    def collect(self, node, collector):
        if node.left:
            self.collect(node.left, collector)
        collector.append(node.val)
        if node.right:
            self.collect(node.right, collector)
```

Version 2:

- Iterative approach

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        stack = []
        result = []

        current = root
        while current or stack:
            while current:
                stack.append(current)
                current = current.left
            
            item = stack.pop()
            result.append(item.val)

            if item.right:
                current = item.right
        
        return result
```