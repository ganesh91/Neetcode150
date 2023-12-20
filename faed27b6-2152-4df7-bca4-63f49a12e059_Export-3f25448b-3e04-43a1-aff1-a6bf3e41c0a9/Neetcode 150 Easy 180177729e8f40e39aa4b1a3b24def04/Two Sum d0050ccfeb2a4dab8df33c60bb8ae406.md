# Two Sum

Status: Not started
Tags: BinarySearch

[https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        nums = [(i,en) for en,i in enumerate(nums)]
        nums.sort(key=lambda x: x[0])
        print(nums)
        for en,i in enumerate(nums):
            search = target-i[0]
            before = self.binary_search(nums, 0, en-1, search)
            if before > 0:
                return [i[1], before]
            after = self.binary_search(nums, en+1, len(nums)-1, search)
            if after > 0:
                return [i[1], after]
        return [-1, -1]
    
    def binary_search(self, arr, low, high, target):
        while low <= high:
            mid = low + (high-low)//2
            if arr[mid][0] == target:
                return arr[mid][1]
            elif arr[mid][0] > target:
                high = mid-1
            else:
                low = mid+1
        return -1
```