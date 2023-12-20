# 1846. Maximum Element After Decreasing and Rearranging

Status: Not started
Tags: Sorting, Stack

[https://leetcode.com/problems/maximum-element-after-decreasing-and-rearranging/](https://leetcode.com/problems/maximum-element-after-decreasing-and-rearranging/)

```python
class Solution:
    def maximumElementAfterDecrementingAndRearranging(self, arr: List[int]) -> int:
        arr.sort()
        arr[0] = 1

        # since its sorted, I knoe the next number is > or atleast the same number
        # [1,2,2,6,4] <- not possible
        # 

        i = 0
        stack = []
        while i < len(arr):
            if len(stack) == 0:
                stack.append(arr[i])
            elif abs(stack[-1]-arr[i]) <= 1:
                stack.append(arr[i])
            else:
                stack.append(stack[-1]+1)
            i+=1
        print(stack)
        return stack[-1]
```