# Clone Graph

Status: Not started
Summary: The "Clone Graph" problem on LeetCode involves cloning a graph represented by a Node class. The given solution uses depth-first search (DFS) to recursively clone the graph. It maintains a node_lookup dictionary to keep track of cloned nodes and a visited set to avoid duplicate cloning. The solution returns the cloned node corresponding to the input node.
Tags: DFS, Hash Map
Last edited time: November 24, 2023 5:26 PM

[https://leetcode.com/problems/clone-graph/](https://leetcode.com/problems/clone-graph/)

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node:
            return node
        node_lookup = {}
        visited = set([])
        self.clone(node, node_lookup, visited)
        return node_lookup[node.val]

    def clone(self, node, node_lookup, visited):
        visited.add(node.val)
        cloned = self.get_or_create(node.val, node_lookup)
        for child in node.neighbors:
            c_child = self.get_or_create(child.val, node_lookup)
            cloned.neighbors.append(c_child)
        for child in node.neighbors:
            if child.val not in visited:
                self.clone(child, node_lookup, visited)
    
    def get_or_create(self, val, node_lookup):
        if val not in node_lookup:
            node_lookup[val] = Node(val)
        return node_lookup[val]
```