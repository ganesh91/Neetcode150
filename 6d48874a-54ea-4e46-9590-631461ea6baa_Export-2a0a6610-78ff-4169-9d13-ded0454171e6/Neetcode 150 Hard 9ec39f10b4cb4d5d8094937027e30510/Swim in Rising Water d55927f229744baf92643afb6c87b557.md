# Swim in Rising Water

Status: Not started
Tags: Minimum Spanning Tree, Prims
Created time: December 20, 2023 3:22 PM

[https://leetcode.com/problems/swim-in-rising-water/submissions/](https://leetcode.com/problems/swim-in-rising-water/submissions/)

```python
class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        min_dist = 0
        seen = set([(0,0)])
        q = [(grid[0][0], 0, 0)]
        ans = 0
        s = len(grid)

        while q:
            distance, row, col = heapq.heappop(q)
            ans = max(ans, distance)
            if row == col == len(grid)-1:
                break
            
            for a,b in [(-1,0), (0, -1), (1, 0), (0, 1)]:
                x,y = row+a, col+b
                if 0 <= x < s and 0 <= y < s and (x,y) not in seen:
                    heapq.heappush(q, (grid[x][y], x, y))
                    seen.add((x,y))
        
        return ans
```