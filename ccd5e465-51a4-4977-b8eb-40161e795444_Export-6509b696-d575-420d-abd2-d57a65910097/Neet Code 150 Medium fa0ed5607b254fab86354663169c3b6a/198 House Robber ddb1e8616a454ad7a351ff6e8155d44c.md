# 198. House Robber

Status: Not started
Tags: Dynamic Programming
Last edited time: November 30, 2023 1:39 PM

[https://leetcode.com/problems/house-robber](https://leetcode.com/problems/house-robber)

Left to Right Approach

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums or len(nums) == 0:
            return 0

        # RR: max((i-2)+i, (i-1))
        for i in range(1, len(nums)):
            if i == 1:
                nums[i] = max(nums[i], nums[i-1])
            else:
                nums[i] = max(nums[i-2]+ nums[i], nums[i-1])
        
        return nums[-1]
```

Right to left Approach:

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums or len(nums) == 0:
            return 0
				for i in range(len(nums)-2, -1, -1):
            if i == len(nums)-2:
                nums[i] = max(nums[i], nums[i+1])
            else:
                nums[i] = max(nums[i+2]+nums[i], nums[i+1])
        
        return nums[0]
```

works only for positive integers