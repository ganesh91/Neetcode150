# 1464. Maximum Product of Two Elements in an Array

Status: Not started
Tags: Array

[https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/](https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/)

```jsx
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        first = 0
        nxt = 0
        for i in nums:
            if i > first:
                nxt = max(nxt, first)
                first = i
            elif i <= first:
                nxt = max(nxt, i)
        return (first-1)*(nxt-1)
```