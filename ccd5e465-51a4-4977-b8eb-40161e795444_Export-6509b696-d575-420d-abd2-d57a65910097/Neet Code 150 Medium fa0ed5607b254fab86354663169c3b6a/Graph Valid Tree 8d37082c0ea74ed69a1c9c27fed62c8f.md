# Graph Valid Tree

Status: Not started
Tags: DFS, UnionFind
Last edited time: November 26, 2023 11:05 AM

[https://leetcode.com/problems/graph-valid-tree/](https://leetcode.com/problems/graph-valid-tree/)

Version 1: Union Find

If the two nodes trying to be unioned in the same tree, then there is a cycle.

We can use unionfind to detect this cycle.

```python
from dataclasses import dataclass

@dataclass
class Entry:
    node: int
    parent: int

class UnionFind:
    def __init__(self):
        self.nodes = {}
        self.collection = {}
    
    def create(self, val):
        node = Entry(val, val)
        self.nodes[val] = node
        self.collection[val] = [node]
        return node
    
    def find(self, node):
        if node not in self.nodes:
            return self.create(node)
        return self.nodes[node]
    
    def union(self, edge1, edge2):
        node1 = self.find(edge1)
        node2 = self.find(edge2)
        if node1.parent == node2.parent:
            return False
        smaller, larger = (node1.parent, node2.parent) if len(self.collection[node1.parent]) < len(self.collection[node2.parent]) else (node2.parent, node1.parent)
        for node in self.collection[smaller]:
            node.parent = larger
            self.collection[larger].append(node)
        del self.collection[smaller]
        return True

class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        uf = UnionFind()
        for i in range(n):
            uf.create(i)
        for edge1, edge2 in edges:
            if not uf.union(edge1, edge2):
                return False
        return len(uf.collection) == 1 and len(uf.collection[uf.find(0).parent]) == n
```

Version 2: DFS with parent tracking

```python
# we can start with any node.
# The intuition is if all nodes are connected, we can reach all of them
# If there is a cycle, we will reach that cycle somehow.
# if the graph is disconnected, then len(visited) != n
```

```python
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        graph = {}
        for i in range(n):
            graph[i] = []
        
        for origin, destination in edges:
            graph[origin].append(destination)
            graph[destination].append(origin)
        
        visited = set([])
        # we can start with any node.
        # The intuition is if all nodes are connected, we can reach all of them
        # If there is a cycle, we will reach that cycle somehow.

        if not self.visit(graph, 0, None, visited):
            return False
        
        return len(visited) == n
    
    def visit(self, graph, current, prev, visited):
        if current in visited:
            return False
        visited.add(current)
        for child in graph[current]:
            if child != prev:
                canvisit = self.visit(graph, child, current, visited)
                if not canvisit:
                    return False
        return True
```