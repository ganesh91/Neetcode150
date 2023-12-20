# 1814. Count Nice Pairs in an Array

Status: Not started
Tags: Hash Map

```python
class Solution:
    def countNicePairs(self, nums: List[int]) -> int:
        revd = [i-self.reverse_digits(i) for i in nums]
        lookup = {}
        counts = 0
        for i in revd:
            if i in lookup:
                counts+=lookup[i]
                lookup[i]+=1
            else:
                lookup[i]=1
        return counts % (10**9+7)
    
    def reverse_digits(self, num):
        result = 0
        # 100 %10 (0)
        while num:
            result = (result * 10) + num %10
            num = num//10
        
        return result
```