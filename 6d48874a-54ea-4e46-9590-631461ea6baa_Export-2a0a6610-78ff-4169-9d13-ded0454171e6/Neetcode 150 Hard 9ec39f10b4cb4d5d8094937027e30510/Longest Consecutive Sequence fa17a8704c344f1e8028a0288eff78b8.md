# Longest Consecutive Sequence

Status: Not started
Tags: HashMap, Sorting
Created time: December 8, 2023 1:52 PM

[https://leetcode.com/problems/longest-consecutive-sequence/](https://leetcode.com/problems/longest-consecutive-sequence/)

Version 1:

- sorting approach

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if len(nums) <= 1:
            return len(nums)
        
        nums.sort()
        print(nums)
        g_max = 0
        c_max = 1

        for i in range(1, len(nums)):
            if nums[i] == nums[i-1]+1:
                c_max += 1
            else:
                g_max = max(g_max, c_max)
                c_max = 1
        g_max = max(g_max, c_max)
        return g_max
```

Version 2:

- lookup approach

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        lookup = set(nums)
        global_max = 0
        for i in nums:
            if i in lookup:
                global_max = max(global_max, 1+self.traverse(lookup, i, 1)+self.traverse(lookup,i,-1))
        
        return global_max
    
    def traverse(self, lookup, current, direction):
        count = 0
        while current+direction in lookup:
            count += 1
            lookup.remove(current+direction)
            current += direction
        return count
```