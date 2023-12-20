# Longest Common Subsequence

Status: Not started
Tags: Dynamic Programming, Memoization
Last edited time: December 5, 2023 11:56 PM

[https://leetcode.com/problems/longest-common-subsequence/](https://leetcode.com/problems/longest-common-subsequence/)

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[-1 for i in range(len(text2))] for j in range(len(text1))]
        res =  self.helper(text1, text2, 0, 0, dp)
        for i in dp:
            print(i)
        return res
    

    def helper(self, text1, text2, l1, l2, dp):
        if l1 >= len(text1) or l2 >= len(text2):
            return 0
        if dp[l1][l2] >= 0:
            return dp[l1][l2]
        # Three options
        matches = 1 if text1[l1] == text2[l2] else 0
        res = None
        if matches:
            return 1 +  self.helper(text1, text2, l1+1, l2+1, dp)
        else:
            res =  max(self.helper(text1, text2, l1+1, l2, dp),
                     self.helper(text1, text2, l1, l2+1, dp))
        dp[l1][l2] = res
        return res
```