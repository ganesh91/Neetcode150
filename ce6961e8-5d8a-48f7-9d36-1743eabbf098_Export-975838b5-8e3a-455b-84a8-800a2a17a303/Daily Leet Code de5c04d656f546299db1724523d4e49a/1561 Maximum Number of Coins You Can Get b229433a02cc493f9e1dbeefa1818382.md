# 1561. Maximum Number of Coins You Can Get

Status: Not started
Tags: Math

```python
from collections import deque
class Solution:
    def maxCoins(self, piles: List[int]) -> int:
        piles.sort()
        coins = 0
        for i in range((len(piles)//3),len(piles),2):
            coins += piles[i]
        return coins
```