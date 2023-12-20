# K Closest Points to Origin

Status: Not started
Tags: Heap
Last edited time: November 28, 2023 5:02 PM

[https://leetcode.com/problems/k-closest-points-to-origin/](https://leetcode.com/problems/k-closest-points-to-origin/)

```python
import heapq
from dataclasses import dataclass, field

@dataclass(order=True)
class Point:
    x: int = field(compare=False)
    y: int = field(compare=False)
    origin: float

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        q = []
        for point in points:
            distance = (point[0]**2 + point[1]**2)**0.5
            if len(q) < k:
                heapq.heappush(q, Point(point[0], point[1], -distance))
            else:
                heapq.heappushpop(q, Point(point[0], point[1], -distance))
        
        return [[point.x, point.y] for point in q]
```