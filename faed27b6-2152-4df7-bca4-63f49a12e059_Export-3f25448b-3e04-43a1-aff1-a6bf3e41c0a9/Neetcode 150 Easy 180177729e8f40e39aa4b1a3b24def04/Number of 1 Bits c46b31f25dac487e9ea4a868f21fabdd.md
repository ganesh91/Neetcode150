# Number of 1 Bits

Status: Not started
Tags: Bit Manipulation

[https://leetcode.com/problems/number-of-1-bits/](https://leetcode.com/problems/number-of-1-bits/)

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        result = []
        while n:
            md = n%2
            div = n//2
            result.append(md)
            n = div
        return sum(result)
```