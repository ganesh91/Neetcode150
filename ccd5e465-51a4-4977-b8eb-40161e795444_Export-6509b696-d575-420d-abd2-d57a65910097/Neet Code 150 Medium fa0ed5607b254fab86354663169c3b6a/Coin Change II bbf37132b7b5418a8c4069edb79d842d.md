# Coin Change II

Status: Not started
Tags: Dynamic Programming
Last edited time: December 2, 2023 6:34 PM

[https://leetcode.com/problems/coin-change-2/](https://leetcode.com/problems/coin-change-2/)

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [[-1 for i in range(len(coins))] for j in range(amount+1)]
        x =  self.recurse(0, amount, coins, 0, dp)
        for i in dp:
            print(i)
        return x
    
    def recurse(self, current, amount, coins, idx, dp):
        if current == amount:
            return 1
        if current > amount or idx >= len(coins):
            return 0
        if dp[current][idx] >= 0:
            return dp[current][idx]
        val =  self.recurse(current+coins[idx], amount, coins, idx, dp) + self.recurse(current, amount, coins, idx+1, dp)
        dp[current][idx] = val
        return val
```