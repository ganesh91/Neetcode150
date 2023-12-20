# 1287. Element Appearing More Than 25% In Sorted Array

Status: Not started
Tags: Binary Search

[https://leetcode.com/problems/element-appearing-more-than-25-in-sorted-array/](https://leetcode.com/problems/element-appearing-more-than-25-in-sorted-array/)

```python
import math
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        low, high = 0, len(arr)-1
        mid = low + (high-low)//2
        left = low + (mid-low)//2
        right = mid + math.ceil((high-mid)/2)
        indices = [mid, left, right]

        mx = 0
        val = 0
        for i in indices:
            right = self.search_right(arr, i)
            left = self.search_left(arr, i)
            diff = right-left+1
            print(f"i: {i}, right: {right}, left: {left}, val: {arr[i]}")
            if diff > mx:
                mx = diff
                val = arr[i]
        return val
    
    def search_left(self, array, index):
        left, right = 0, index
        while left < right:
            mid = left + (right-left)//2
            if array[mid] < array[index]:
                left = mid+1
            else:
                right = mid
        return left
    
    def search_right(self, array, index):
        left, right = index, len(array)-1
        while left < right:
            mid = left + (right-left)//2
            if array[mid] > array[index]:
                right = mid
            else:
                left = mid+1
        if array[right] != array[index]:
            return left -1
        return left
```

Version 2:

```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        i = 0
        repeats = (len(arr))//4

        while i < len(arr)-repeats:
            if arr[i] == arr[i+repeats]:
                return arr[i]
            i+=1
```