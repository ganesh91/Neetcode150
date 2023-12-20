# Gas Station

Status: Not started
Tags: Greedy, Preprocessing
Last edited time: December 3, 2023 9:39 PM

[https://leetcode.com/problems/gas-station/](https://leetcode.com/problems/gas-station/)

Idea:

- Brute force o(n2)
- for every point, traverse and check

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
				is_complete = False
        for i in range(len(gas)):
            if self.visit(gas, cost, i, 0, 0):
                return i
        return -1

    def visit(self, gas, cost, index, rgas, visits):
        if visits == len(gas):
            return True
        complete = False
        i = index % len(gas)
        nxt = (i+1) % len(gas)
        gauge = rgas + gas[i]
        if gauge-cost[i] >= 0:
            complete = complete or self.visit(gas, cost, i+1, gauge-cost[i], visits+1)
        return complete
```

- Rather than n2, preprocess to calculate gain.
- so if we have gas and can process progress, else start again
- Maximum travel need is 2*n

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        dp = []
        for i in range(len(gas)):
            dp.append(gas[i]-cost[i])

        start = 0
        current = 0
        reserve = 0

        while current < 2*len(gas):
            i = current % len(gas)
            while current > i and start == i and reserve >= 0:
                return i
            if reserve <= 0:
                start = i
                reserve = 0
            reserve += dp[i]
            current += 1
        
        return -1
```