# 2956. Find Common Elements Between Two Arrays

Status: Not started
Tags: Array

```python
class Solution:
    def findIntersectionValues(self, nums1: List[int], nums2: List[int]) -> List[int]:
        lookup_1 = set(nums1)
        lookup_2 = set(nums2)
        f = sum([1 if (i in lookup_2) else 0 for i in nums1])
        s = sum([1 if (i in lookup_1) else 0 for i in nums2])
        return [f,s]
```