# Longest Increasing Subsequence

Status: Not started
Tags: Dynamic Programming
Last edited time: December 2, 2023 2:10 PM

[https://leetcode.com/problems/longest-increasing-subsequence/](https://leetcode.com/problems/longest-increasing-subsequence/)

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        cache = [-1 for i in range(len(nums))]
        cache[-1] = 1
        for i in range(len(nums)):
            if cache[i] == -1:
                self.search(nums, i, cache)
        return max(cache)
    
    def search(self, nums, i, cache):
        if cache[i] >= 0:
            return cache[i]
        length = 1
        for j in range(i+1, len(nums)):
            if nums[j] > nums[i]:
                length = max(length, self.search(nums, j, cache)+1)
        cache[i] = length
        return length
```