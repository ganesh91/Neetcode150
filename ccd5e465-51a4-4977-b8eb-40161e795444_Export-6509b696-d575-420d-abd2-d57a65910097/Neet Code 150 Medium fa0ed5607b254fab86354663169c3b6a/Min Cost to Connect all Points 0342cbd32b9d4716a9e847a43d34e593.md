# Min Cost to Connect all Points

Status: Not started
Tags: UnionFind
Last edited time: November 29, 2023 6:01 PM

[https://leetcode.com/problems/min-cost-to-connect-all-points](https://leetcode.com/problems/min-cost-to-connect-all-points)

```python
from dataclasses import dataclass, field
import heapq

@dataclass
class Entry:
    element: int
    parent: int

@dataclass(order=True)
class Point:
    a: int = field(compare=False)
    b: int = field(compare=False)
    cost: int

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
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        q = []
        for i in range(len(points)):
            for j in range(i+1, len(points)):
                a = points[i]
                b = points[j]
                dist = abs(a[0]-b[0]) + abs(a[1]-b[1])
                heapq.heappush(q, Point(i,j,dist))
        
        uf = UnionFind(len(points))

        cost = 0
        while len(uf.graph) > 1:
            shortest = heapq.heappop(q)
            if uf.find(shortest.a).parent != uf.find(shortest.b).parent:
                cost += shortest.cost
                uf.union(shortest.a, shortest.b)
        
        return cost
```