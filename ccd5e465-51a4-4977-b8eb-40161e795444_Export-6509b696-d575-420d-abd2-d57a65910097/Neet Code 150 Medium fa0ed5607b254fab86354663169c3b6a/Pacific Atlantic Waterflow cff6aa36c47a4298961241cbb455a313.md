# Pacific Atlantic Waterflow

Status: Not started
Summary: The document provides a Python solution for the problem of determining the cells in a matrix that can flow to both the Pacific and Atlantic Oceans. The solution uses a recursive approach to mark the cells and returns the coordinates of the marked cells.
Tags: DFS
Last edited time: November 24, 2023 11:01 AM

[https://leetcode.com/problems/pacific-atlantic-water-flow/](https://leetcode.com/problems/pacific-atlantic-water-flow/)

```python
class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        cache = [[-1 for _ in range(len(heights[0]))] for _ in range(len(heights))]
        print(heights, cache)

        result = []
        for i in range(len(heights)):
            for j in range(len(heights[0])):
                value = self.mark(heights, cache, i, j)
                if value == 3:
                    result.append([i,j])
        return result
    
    def mark(self, heights, cache, i, j):
        if cache[i][j] > -1:
            return cache[i][j]
        cache[i][j] = 0
        result = []
        for a,b in [(0,-1), (-1, 0), (1, 0), (0,1)]:
            x, y = i+a, j+b
            if x <0 or y<0:
                result.append(1)
            elif x >= len(heights) or y >= len(heights[0]):
                result.append(2)
            elif heights[x][y] <= heights[i][j]:
                result.append(self.mark(heights, cache, x, y))
        
        if 3 in result or (1 in result and 2 in result):
            cache[i][j] = 3
        elif 1 in result:
            cache[i][j] = 1
        elif 2 in result:
            cache[i][j] = 2
        else:
            cache[i][j] = -1
        return cache[i][j]
```