# Serialize and Deserialize Binary Tree

Status: Not started
Tags: BFS
Created time: December 19, 2023 5:10 PM

[https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)

```python
from collections import deque
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        result = []
        q = deque([[root]])
        while q:
            level = []
            curr = q.popleft()
            for i in curr:
                if i:
                    level.append(i.left)
                    level.append(i.right)
                result.append(i.val if i else None)
            if len(level) > 0:
                q.append(level)
        while result and result[-1] is None:
            result.pop()
        csv =  ",".join([str(i) for i in result])
        return csv

        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        csv = deque(data.split(","))
        if csv[0] == '':
            return None
        root = TreeNode(csv.popleft())
        q = [[root]]
        while q:
            level = q.pop()
            nxt = []
            for i in level:
                left = csv.popleft() if csv else None
                right = csv.popleft() if csv else None
                if left and left != 'None':
                    i.left = TreeNode(int(left))
                    nxt.append(i.left)
                if right and right != 'None':
                    i.right = TreeNode(int(right))
                    nxt.append(i.right)
            if len(nxt) > 0:
                q.append(nxt)
        return root

        
        

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```