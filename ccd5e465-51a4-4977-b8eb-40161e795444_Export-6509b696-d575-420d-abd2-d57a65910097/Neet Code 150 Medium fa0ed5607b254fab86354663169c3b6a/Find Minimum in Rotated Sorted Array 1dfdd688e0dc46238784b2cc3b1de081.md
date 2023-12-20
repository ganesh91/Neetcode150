# Find Minimum in Rotated Sorted Array

Status: Not started
Tags: Binary Search
Last edited time: November 26, 2023 1:31 PM

[https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

Version 1:

- start +1 < mid version
- Post processing for 2 length array

```python
def findMin(self, nums: List[int]) -> int:
        start, end = 0, len(nums)-1
        while start+1 < end:
            mid = start + (end-start)//2
            if nums[mid] < nums[start]:
                end = mid
            elif nums[mid] > nums[end]:
                start = mid
            else:
                end = mid-1
        if nums[start] < nums[end]:
            return nums[start]
        return nums[end]
```

Version 2:

- pre-processing for un-sorted.
- binary search on the rest

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        if nums[0] <= nums[-1]:
            return nums[0]
        start, end = 0, len(nums)-1
        while start < end:
            mid = start + (end-start)//2
            if nums[start] < nums[mid]:
                start = mid
            else:
                end = mid
        return nums[start+1]
```