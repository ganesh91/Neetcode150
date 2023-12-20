# 1716. Calculate Money in Leetcode Bank

Status: Not started
Tags: Math

[https://leetcode.com/problems/calculate-money-in-leetcode-bank/](https://leetcode.com/problems/calculate-money-in-leetcode-bank/)

```python
class Solution:
    def totalMoney(self, n: int) -> int:
        credit = 0
        current = 0
        while current < n:
            credit += (current // 7) + (current % 7)+1
            current += 1
        return credit
```