# Unique Paths

Status: Not started
Tags: Dynamic Programming, Recursion
Last edited time: December 5, 2023 4:38 PM

[https://leetcode.com/problems/unique-paths/](https://leetcode.com/problems/unique-paths/)

Version 1:

- Recursive Method

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
				dp = [[float('inf') for _ in range(n)] for _ in range(m)]
        dp[m-1][n-1]=1
        return self.compute(0,0,dp)
    
    def compute(self, row, col, dp):
        if dp[row][col] < float('inf'):
            return dp[row][col]
        mv = 0
        if row+1 < len(dp):
            mv += self.compute(row+1, col, dp)
        if col+1 < len(dp[row]):
            mv += self.compute(row, col+1, dp)
        dp[row][col] = mv
        return mv
```

Version 2:

- Iterative method

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0 for i in range(n)] for j in range(m)]
        for i in range(m):
            dp[i][n-1] = 1
        for j in range(n):
            dp[m-1][j] = 1
        
        for row in range(m-2,-1,-1):
            for column in range(n-2, -1, -1):
                dp[row][column] = dp[row][column+1] + dp[row+1][column]
        
        return dp[0][0]
```