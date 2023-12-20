# Kth Largest Element in an Array

Status: Not started
Tags: Heap, QuickSelect, QuickSort
Last edited time: November 28, 2023 5:01 PM

[https://leetcode.com/problems/kth-largest-element-in-an-array/](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Version 1:

- Min Heap

```python
import heapq
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        q = []
        for en,i in enumerate(nums):
            if len(q) < k:
                heapq.heappush(q, (i, en))
            else:
                heapq.heappushpop(q, (i,en))
        return q[0][0]
```

<aside>
💡 Version 2: quick select

</aside>

```
import heapq
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return self.quickselect(nums, len(nums) - k, 0, len(nums)-1)
    
    def quickselect(self, arr, k, start,end):
        pivot = start
        l,r = start+1, end
        while r >= l:
            if arr[l] <= arr[pivot]:
                l += 1
            elif arr[r] > arr[pivot]:
                r -=1
            elif arr[l] >  arr[pivot] and arr[r] <= arr[pivot]:
                arr[l], arr[r] = arr[r], arr[l]
                l += 1
                r -= 1
        arr[pivot], arr[r] = arr[r], arr[pivot]
        if k == r:
            return arr[r]
        elif k < r:
            return self.quickselect(arr, k, start, r-1)
        else:
            return self.quickselect(arr, k, r+1, end)
```