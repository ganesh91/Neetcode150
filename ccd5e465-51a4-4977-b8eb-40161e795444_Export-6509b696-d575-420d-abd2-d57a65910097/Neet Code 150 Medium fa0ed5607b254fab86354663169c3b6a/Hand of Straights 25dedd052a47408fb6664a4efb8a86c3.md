# Hand of Straights

Status: Not started
Tags: Hash Map, Sorting
Last edited time: December 5, 2023 10:54 AM

[https://leetcode.com/problems/hand-of-straights/](https://leetcode.com/problems/hand-of-straights/)

```python
from collections import deque
class Solution:
    def isNStraightHand(self, hand: List[int], groupSize: int) -> bool:
        lookup = {}
        for i in hand:
            if i not in lookup:
                lookup[i] = 1
            else:
                lookup[i] += 1
        
        hand.sort()
        for i in hand:
            is_straight = True
            for h in range(groupSize):
                if i+h not in lookup:
                    is_straight = False
                    break
            
            if is_straight:
                for h in range(groupSize):
                    if lookup[i+h] <= 1:
                        del lookup[i+h]
                    else:
                        lookup[i+h]-=1
        
        return len(lookup) == 0
```