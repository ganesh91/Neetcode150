# Kth Smallest Element in a BST

Status: Not started
Tags: Array, Stack
Last edited time: November 24, 2023 5:29 PM

[https://leetcode.com/problems/kth-smallest-element-in-a-bst/](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

Idea:

- Flatten out to an array and return
- Iteratively visit using stack

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        result = []
        while True:
            while root:
                stack.append(root)
                root = root.left
            if not stack:
                break
            root = stack.pop()
            result.append(root.val)
            root = root.right

        return result[k-1]
```

Idea:

- If there is element, then visit element.left
- If not element.left, pop it and increment counter
- visit root.right