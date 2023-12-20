# Insert Interval

Status: Not started
Tags: Intervals
Last edited time: December 5, 2023 11:27 AM

[https://leetcode.com/problems/insert-interval/](https://leetcode.com/problems/insert-interval/)

```python
from collections import deque
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        result = []

        original = deque(intervals)
        merge = deque([newInterval])

        while original or merge:
            head = None
            if len(original) > 0 and len(merge) > 0:
                head = original.popleft() if original[0][0] < merge[0][0] else merge.popleft()
            elif len(original) > 0:
                head = original.popleft()
            else:
                head = merge.popleft()
            
            if len(result) == 0:
                result.append(head)
            elif self.hasOverlap(result[-1], head):
                last = result.pop()
                result.append(self.merge(last, head))
            else:
                result.append(head)
        
        return result

    def hasOverlap(self, i1, i2):
        return i1[0] <= i2[0] <= i1[1] or i2[0] <= i1[0] <= i2[1]
    
    def merge(self, i1, i2):
        return [min(i1[0], i2[0]), max(i1[1], i2[1])]
```