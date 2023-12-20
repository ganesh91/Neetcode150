# Find the Duplicate Number

Status: Not started
Tags: Array
Last edited time: November 25, 2023 9:02 PM

[https://leetcode.com/problems/find-the-duplicate-number/description/](https://leetcode.com/problems/find-the-duplicate-number/description/)

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        for i in range(len(nums)):
            target = abs(nums[i])
            if nums[target] < 0:
                return target
            else:
                nums[target] = -nums[target]
        return -1
```

Idea: 

- Mark the value index as negative
- If there were any repetitive node, we would encounter a negative