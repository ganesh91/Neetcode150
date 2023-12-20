# Maximum Product Subarray

Status: Not started
Summary: The "Maximum Product Subarray" problem can be solved using a modified version of the Kadane's algorithm. By keeping track of both the maximum and minimum product so far, we can handle negative numbers. The provided Python solution implements this algorithm to find the maximum product subarray.
Tags: Greedy
Last edited time: November 24, 2023 9:16 AM

[https://leetcode.com/problems/maximum-product-subarray/submissions/](https://leetcode.com/problems/maximum-product-subarray/submissions/)

Idea:

- In Kadane we break when if we add the current element, the current element ≤ 0
- Here, we do the same thing, however since -1 * -1 = +1, we keep track of the negatives as well.

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        max_so_far = nums[0]
        min_so_far = nums[0]
        running = nums[0]
        for i in range(1,len(nums)):
            current = nums[i]
            max_so_far_current = max(current, max_so_far * current, min_so_far * current)
            min_so_far = min(current, min_so_far * current, max_so_far * current)
            max_so_far = max_so_far_current
            running = max(running, max_so_far)
        return running
```