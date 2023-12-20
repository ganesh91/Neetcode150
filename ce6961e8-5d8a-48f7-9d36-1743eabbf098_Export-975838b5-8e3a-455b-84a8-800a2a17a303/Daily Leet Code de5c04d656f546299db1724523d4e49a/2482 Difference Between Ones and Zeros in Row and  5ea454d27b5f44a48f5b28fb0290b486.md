# 2482. Difference Between Ones and Zeros in Row and Column

Status: Not started
Tags: Array

```jsx
class Solution:
    def onesMinusZeros(self, grid: List[List[int]]) -> List[List[int]]:
        rows = len(grid)
        cols = len(grid[0])
        result = [[0 for i in range(cols)] for j in range(rows)]
        
        rsum = [0 for i in range(rows)]
        csum = [0 for i in range(cols)]
        
        for row in range(rows):
            for col in range(cols):
                rsum[row] += grid[row][col]
                csum[col] += grid[row][col]
        
        for row in range(rows):
            for col in range(cols):
                result[row][col] = rsum[row] + csum[col] - (rows-rsum[row]) - (cols-csum[col])
        
        return result
```