# 2958. Length of Longest Subarray With at Most K Frequency

Status: Not started
Tags: Two Pointer

```python
from collections import defaultdict
class Solution:
    def maxSubarrayLength(self, nums: List[int], k: int) -> int:
        start, current = 0,0
        lookup = defaultdict(int)
        max_len = 0
        while current < len(nums):
            if lookup[nums[current]] < k:
                lookup[nums[current]] += 1
                current += 1
            else:
                print(max_len, current - start, current, start)
                max_len = max(max_len, current-start)
                while lookup[nums[current]] >= k:
                    lookup[nums[start]] -= 1
                    start += 1
        max_len = max(max_len, current-start)
        return max_len
```