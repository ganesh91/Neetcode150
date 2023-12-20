# Pow(x, n)

Status: Not started
Tags: Divide and Conquer
Last edited time: November 27, 2023 5:03 PM

[https://leetcode.com/problems/powx-n/submissions/](https://leetcode.com/problems/powx-n/submissions/)

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        abs_n = abs(n)
        is_neg_n = n < 0
        value = self.recurse(x, abs_n)
        if is_neg_n:
            value = 1/value
        return value
    

    @cache
    def recurse(self, x, n):
        if n == 0:
            return 1
        if n == 1:
            return x
        product = 0
        if n%2 == 0:
            half = self.recurse(x, n//2)
            product =  half * half
        else:
            half = self.recurse(x, n//2)
            product =  half * half * x
        return product
```