# Interleaving String

Status: Not started
Tags: Dynamic Programming
Last edited time: December 2, 2023 7:16 PM

[https://leetcode.com/problems/interleaving-string/](https://leetcode.com/problems/interleaving-string/)

```
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False
        dp = [[None for _ in range(len(s2))] for _ in range(len(s1))]
        return self.interleave(s1,0,s2,0,s3,0, dp)
    

    def interleave(self, s1, i, s2, j, s3, k, dp):
        if k >= len(s3):
            return True
        if (i >= len(s1) and s2[j:] == s3[k:]) or (j >= len(s2) and s1[i:] == s3[k:]):
            return True
        if i >= len(s1) or j >= len(s2):
            return False
        if dp[i][j] is not None:
            print("cache Hit")
            return dp[i][j]
        caninterleave = False
        if s1[i] == s3[k]:
            caninterleave = caninterleave or self.interleave(s1, i+1, s2, j, s3, k+1, dp)
        if not caninterleave and s2[j] == s3[k]:
            caninterleave = caninterleave or self.interleave(s1, i, s2, j+1, s3, k+1, dp)
        dp[i][j]=caninterleave
        return caninterleave
```