# Permutations

Status: Not started
Tags: BackTracking
Last edited time: November 26, 2023 5:36 PM

[https://leetcode.com/problems/permutations/](https://leetcode.com/problems/permutations/)

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        result = []
        self.helper(nums, 0, result)
        return result
    

    def helper(self, nums, index, result):
        if index >= len(nums):
            result.append([i for i in nums])
            return
        for i in range(index, len(nums)):
            nums[index], nums[i] = nums[i], nums[index]
            self.helper(nums, index+1, result)
            nums[index], nums[i] = nums[i], nums[index]
```