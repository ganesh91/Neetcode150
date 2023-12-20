# Min Cost Climbing Stairs

Status: Not started
Tags: Dynamic Programming

[https://leetcode.com/problems/min-cost-climbing-stairs/](https://leetcode.com/problems/min-cost-climbing-stairs/)

Recursive approach

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        dp = [-1 for i in range(len(cost))]
        return min(self.jump(0, cost, dp), self.jump(1,cost, dp))
    
    def jump(self, index, cost, dp):
        if index >= len(cost):
            return 0
        if dp[index] >= 0:
            return dp[index]
        cost = cost[index]+min(self.jump(index+1, cost, dp), self.jump(index+2, cost, dp))
        dp[index] = cost
        return cost
```

Iterative approach

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        for i in range(len(cost)-3, -1, -1):
            cost[i] = cost[i] + min(cost[i+1], cost[i+2])
        return min(cost[0], cost[1])
```