# Edit Distance

Status: Not started
Tags: Dynamic Programming, Memoization
Created time: December 8, 2023 3:39 PM

[https://leetcode.com/problems/edit-distance/](https://leetcode.com/problems/edit-distance/)

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        dp = [[-1 for i in range(len(word2))] for _ in range(len(word1))]
        return self.distance(word1, word2, 0, 0, dp)
    

    def distance(self, word1, word2, i, j, dp):
        if i >= len(word1) and j >= len(word2):
            return 0
        if i >= len(word1):
            return len(word2[j:])
        if j >= len(word2):
            return len(word1[i:])
        if dp[i][j] >= 0:
            return dp[i][j]
        if word1[i] == word2[j]:
            dp[i][j] = self.distance(word1, word2, i+1, j+1, dp)
        else:
            dp[i][j] = 1+min([self.distance(word1, word2, i, j+1, dp),
            self.distance(word1, word2, i+1, j, dp),
            self.distance(word1, word2, i+1, j+1, dp),
            ])
        return dp[i][j]
```