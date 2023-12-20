# 1650. Lowest Common Ancestor of a Binary Tree III

Status: Not started
Tags: Hash Map

[https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/)

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.parent = None
"""

class Solution:
    def lowestCommonAncestor(self, p: 'Node', q: 'Node') -> 'Node':
        if self.isChild(p,q):
            return p
        if self.isChild(q, p):
            return q
        # Since we have rule out the nodes being parents of each other the parents must
        # be in the parent only
        path_to_root = set([])
        while p:
            path_to_root.add(p)
            p = p.parent
        
        while q:
            if q in path_to_root:
                return q
            q = q.parent

    def isChild(self, p, q):
        if p == q:
            return True
        if not p:
            return False
        return self.isChild(p.left, q) or self.isChild(p.right, q)
```