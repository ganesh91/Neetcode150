# Number of Connected Components in Graph

Status: Not started
Summary: This document discusses two variants for finding the number of connected components in an undirected graph. Variant 1 uses a typical DFS approach, while Variant 2 utilizes the Union Find algorithm. Both variants provide solutions to the problem.
Tags: DFS, UnionFind
Last edited time: November 24, 2023 9:54 AM

[https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/description/](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/description/)

Variant 1:

- Typical DFS. Create a graph and do DFS to mark islands.

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        graph = {}
        for i in range(n):
            graph[i]=[]
        for x,y in edges:
            graph[x].append(y)
            graph[y].append(x)
        return self.dfs_variant(graph)
    

    def dfs_variant(self, graph):
        islands = 0
        visited = set([])
        for i in graph:
            if i not in visited:
                islands += 1
                self.visit(graph, i, visited)
        
        return islands
    
    def visit(self, graph, node, visited):
        visited.add(node)
        for child in graph[node]:
            if child not in visited:
                self.visit(graph, child, visited)
```

Variant 2:

Union Find:

```python
from dataclasses import dataclass

@dataclass
class Entry:
    element: int
    parent: int

class UnionFind:
    def __init__(self, n):
        self.lookup = {}
        self.graph = {}
        for i in range(n):
            item = Entry(i,i)
            self.lookup[i] = item
            self.graph[i] = [item]
    
    def find(self, i):
        return self.lookup[i]
    
    def union(self, i, j):
        head_i = self.find(i).parent
        head_j = self.find(j).parent
        if head_i != head_j:
            larger_head = head_i if len(self.graph[head_i]) > len(self.graph[head_j]) else head_j
            smaller_head = head_i if len(self.graph[head_i]) <= len(self.graph[head_j]) else head_j
            for element in self.graph[smaller_head]:
                element.parent = larger_head
                self.graph[larger_head].append(element)
            del self.graph[smaller_head]

class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        union_find = UnionFind(n)
        for i in range(n):
            print(union_find.find(i))
        for i,j in edges:
            union_find.union(i,j)
        
        return len(union_find.graph)
```