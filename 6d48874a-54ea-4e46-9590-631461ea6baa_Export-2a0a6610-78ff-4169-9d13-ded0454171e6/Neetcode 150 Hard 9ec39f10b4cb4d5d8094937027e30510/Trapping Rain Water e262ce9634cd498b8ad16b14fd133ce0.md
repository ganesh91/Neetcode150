# Trapping Rain Water

Status: Not started
Tags: Two Pointers
Created time: December 16, 2023 7:41 PM

[https://leetcode.com/problems/trapping-rain-water/description/](https://leetcode.com/problems/trapping-rain-water/description/)

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        
        s = 0
        while s < len(height) and height[s] <= 0:
            s += 1
        
        area = 0
        c = s+1
        
        while c < len(height):
            if height[c] >= height[s]:
                common_height = min(height[c], height[s])
                while s < c:
                    curr = min(common_height, height[s])
                    ic = (common_height-curr)
                    area += ic
                    s+=1
            c += 1
        
        e = len(height)-1
        while e >= 0 and height[e] <= 0:
            e-= 1
        
        c = e-1

        while c >= 0:
            if height[c] > height[e]:
                common_height = min(height[c], height[e])
                while c < e:
                    curr = min(common_height, height[e])
                    ic = (common_height-curr)
                    area += ic
                    e-=1
            c -= 1
        
        return area
```