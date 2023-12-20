# Coin Change

Status: Not started
Tags: Dynamic Programming
Last edited time: November 30, 2023 6:41 PM

[https://leetcode.com/problems/coin-change/](https://leetcode.com/problems/coin-change/)

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf') for i in range(amount+1)]
        dp[0] = 0
        
        for i in range(amount+1):
            for j in coins:
                if i-j >= 0:
                    dp[i] = min(dp[i], dp[i-j]+1)
        
        print(dp)
        return dp[amount] if dp[amount] < float('inf') else -1
```