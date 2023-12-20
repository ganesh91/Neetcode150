# Sliding Window Maximum

Status: Not started
Tags: Heaps
Created time: December 16, 2023 2:37 PM

[https://leetcode.com/problems/sliding-window-maximum/description/](https://leetcode.com/problems/sliding-window-maximum/description/)

```python
import heapq
from dataclasses import dataclass, field

@dataclass(order=True)
class Entry:
    index: int = field(compare=False)
    val: int

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        result = []
        q = []
        idx = 0
        while idx < len(nums):
            if idx < k-1:
                heapq.heappush(q, Entry(idx, -nums[idx]))
            else:
                heapq.heappush(q, Entry(idx, -nums[idx]))
                result.append(self.extract_max(q, idx, k))
            idx += 1

        return result

    def extract_max(self, q, idx, k):
        while q[0].index <= idx-k:
            heapq.heappop(q)
        return -q[0].val
```