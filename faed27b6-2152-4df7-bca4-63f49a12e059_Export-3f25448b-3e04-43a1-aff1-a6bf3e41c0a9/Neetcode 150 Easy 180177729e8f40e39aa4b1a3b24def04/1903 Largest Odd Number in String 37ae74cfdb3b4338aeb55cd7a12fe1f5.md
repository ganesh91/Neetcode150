# 1903. Largest Odd Number in String

Status: Not started
Tags: String

[https://leetcode.com/problems/largest-odd-number-in-string/](https://leetcode.com/problems/largest-odd-number-in-string/)

```python
class Solution:
    def largestOddNumber(self, num: str) -> str:
        for i in range(len(num)-1, -1 ,-1):
            if int(num[i]) % 2 != 0:
                return num[:i+1]
        return ""
```