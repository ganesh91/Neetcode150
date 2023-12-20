# Partition Equal Subset Sum

Status: Not started
Tags: Dynamic Programming, Memoization, Recursion
Last edited time: December 1, 2023 11:19 AM

[https://leetcode.com/problems/partition-equal-subset-sum](https://leetcode.com/problems/partition-equal-subset-sum)

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        total = sum(nums)
        if total % 2 != 0:
            return False
        k = total//2

        cache = [[-1 for i in range(len(nums)+1)] for i in range(k+1)]
        result = self.partition(nums, 0, 0, k, cache)
        return result
    
    def partition(self, nums, index, current, target, cache):
        if current == target:
            cache[current][index] = 1
            return True
        if index >= len(nums) or current > target:
            return False
        if cache[current][index] > -1:
            return cache[target][index] == 1
        canpartition = self.partition(nums, index+1, current+nums[index], target, cache)
        if not canpartition:
            canpartition = self.partition(nums, index+1, current, target, cache)
        cache[current][index] = 1 if canpartition else 0
        return canpartition
```