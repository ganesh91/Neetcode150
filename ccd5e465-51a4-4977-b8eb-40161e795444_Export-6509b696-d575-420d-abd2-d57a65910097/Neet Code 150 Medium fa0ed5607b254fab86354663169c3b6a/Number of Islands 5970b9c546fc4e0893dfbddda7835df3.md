# Number of Islands

Status: Not started
Tags: DFS
Last edited time: November 24, 2023 11:09 AM

[https://leetcode.com/problems/number-of-islands/](https://leetcode.com/problems/number-of-islands/)

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        islands = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == "1":
                    islands += 1
                    self.visit(grid, i, j)
        return islands
        
    
    def visit(self, grid, i, j):
        grid[i][j] = "0"
        for (x,y) in [(-1,0),(0,-1), (1,0), (0,1)]:
            a,b = i+x, j+y
            if 0 <= a < len(grid) and 0 <= b < len(grid[0]) and grid[a][b] == "1":
                self.visit(grid, a, b)
```