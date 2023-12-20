# Maximum Subarray

Status: Not started
Summary: The maximum subarray problem is solved using a dynamic programming approach. The algorithm iterates through the array, keeping track of the maximum sum encountered so far and the current sum. If the current sum plus the current element is less than the current element, it marks an inflection point and starts a new subarray. The algorithm returns the maximum sum encountered.
Tags: Greedy
Last edited time: November 24, 2023 9:21 AM

[https://leetcode.com/problems/maximum-subarray/](https://leetcode.com/problems/maximum-subarray/)

Idea:

- if sum so far + current < current: That’s the inflection point and needs a break
- Then continue searching for maximum sum

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        max_so_far = nums[0]
        current = nums[0]
        for i in range(1, len(nums)):
            num = nums[i]
            if current + num < num:
                current = num
            else:
                current += num
            max_so_far = max(current, max_so_far)
        return max_so_far
```