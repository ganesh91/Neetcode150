# Missing Number

Status: Not started
Tags: Binary Search

[https://leetcode.com/problems/missing-number/](https://leetcode.com/problems/missing-number/)

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        nums.sort()
        start, end = 0,len(nums)-1
        while start < end:
            mid = start + (end-start)//2
            if nums[mid] == mid:
                start = mid+1
            else:
                end = mid
        if end == len(nums)-1 and nums[end] == len(nums)-1:
            return end+1
        return end
```