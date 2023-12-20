# Burst Balloons

Status: Not started
Tags: Dynamic Programming
Created time: December 20, 2023 11:03 AM

[https://leetcode.com/problems/regular-expression-matching/description/](https://leetcode.com/problems/regular-expression-matching/description/)

```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        dp = [[float('inf') for i in range(len(nums))] for j in range(len(nums))]
        x =  self.recurse(nums, 0, len(nums)-1, dp)
        return x
    
    def recurse(self, nums, left, right, dp):
        if right < left:
            return 0
        if dp[left][right] < float('inf'):
            return dp[left][right]
        mval = 0
        for i in range(left, right+1):
            lc = 1 if left == 0 else nums[left-1]
            rc = 1 if right >= len(nums)-1 else nums[right+1]
            s = nums[i]
            mval = max(mval, (lc*rc*s)+self.recurse(nums, left, i-1, dp)+self.recurse(nums, i+1, right, dp))
        dp[left][right] = mval
        return mval
```

<aside>
💡 If the dp states are changing, see if you can set the boundary of satates in such a way that sub problems don’t have changing states.

</aside>