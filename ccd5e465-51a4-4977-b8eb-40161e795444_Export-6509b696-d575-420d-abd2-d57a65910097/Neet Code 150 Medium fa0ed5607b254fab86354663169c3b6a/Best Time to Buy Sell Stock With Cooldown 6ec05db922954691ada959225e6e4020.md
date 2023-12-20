# Best Time to Buy/Sell Stock With Cooldown

Status: Not started
Tags: Dynamic Programming
Last edited time: December 5, 2023 2:38 PM

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        cache = [None for i in range(len(prices))]
        return self.calculate(0, prices, cache)
    
    def calculate(self, index, prices, cache):
        if index >= len(prices):
            return 0
        if cache[index] is not None:
            return cache[index]
        profit = 0
        for i in range(index+1, len(prices)):
            if prices[index] < prices[i]:
                profit = max(profit, prices[i]-prices[index]+self.calculate(i+2, prices, cache))
        profit = max(profit, self.calculate(index+1, prices, cache))
        cache[index] = profit
        return profit
```