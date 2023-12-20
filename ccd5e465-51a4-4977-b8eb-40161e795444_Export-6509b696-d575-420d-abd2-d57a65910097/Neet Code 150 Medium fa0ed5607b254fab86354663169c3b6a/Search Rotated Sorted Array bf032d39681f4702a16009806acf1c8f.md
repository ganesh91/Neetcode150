# Search Rotated Sorted Array

Status: Not started
Tags: Binary Search
Last edited time: November 26, 2023 1:45 PM

[https://leetcode.com/problems/search-in-rotated-sorted-array/](https://leetcode.com/problems/search-in-rotated-sorted-array/)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        pivot = self.findpivot(nums)
        print(f"pivot: {pivot}")
        if pivot == 0:
            return self.bsearch(nums, target, 0, len(nums)-1)
        if nums[0] <= target <= nums[pivot-1]:
            return self.bsearch(nums, target, 0, pivot)
        return self.bsearch(nums, target, pivot, len(nums)-1)
    
    def bsearch(self, nums, target, start, end):
        print(f"bounds: {start},{end}")
        while start <= end:
            mid = start + (end-start)//2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                end = mid-1
            else:
                start = mid+1
        return -1

    def findpivot(self, nums):
        if nums[0] <= nums [-1]:
            return 0
        start, end = 0, len(nums)-1
        while start < end:
            mid = start + (end-start)//2
            if nums[start] < nums[mid]:
                start = mid
            else:
                end = mid
        return start+1
```