# Container with Most Water

Status: Not started
Tags: Two Pointers
Last edited time: November 29, 2023 2:33 PM

[https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/)

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        start, end = 0, len(height)-1
        area = 0
        while start < end:
            area = max(area, min(height[start], height[end])*(end-start))
            if height[start] < height[end]:
                start += 1
            else:
                end -= 1
        return area
```