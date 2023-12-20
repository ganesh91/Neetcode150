# Max Area of Island

Status: Not started
Tags: BFS, DFS
Last edited time: November 26, 2023 10:07 AM

[https://leetcode.com/problems/max-area-of-island/description/](https://leetcode.com/problems/max-area-of-island/description/)

DFS:

```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        max_area = 0
        for row in range(len(grid)):
            for column in range(len(grid[0])):
                if grid[row][column] == 1:
                    grid[row][column] = 0
                    max_area = max(max_area, self.calculate_area(grid, row, column))
        return max_area

    def calculate_area(self, grid, row, column):
        area = 1
        for x,y in [(-1,0), (0,-1), (1,0), (0,1)]:
            i = row+x
            j = column+y
            if 0 <= i < len(grid) and 0 <= j < len(grid[0]) and grid[i][j] == 1:
                grid[i][j] = 0
                area += self.calculate_area(grid, i, j)
        return area
```