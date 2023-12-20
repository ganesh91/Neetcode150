# Multiply Strings

Status: Not started
Tags: Math
Last edited time: December 19, 2023 1:50 PM

[https://leetcode.com/problems/multiply-strings/description/](https://leetcode.com/problems/multiply-strings/description/)

```python
from collections import deque
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        smaller, larger = (num1, num2) if len(num1) < len(num2) else (num2, num1)
        lookup = {str(i): i for i in range(10)}

        smaller = deque([lookup[i] for i in smaller])
        larger = [lookup[i] for i in larger]

        while smaller:
            a = smaller.popleft()
            if a != 0:
                smaller.appendleft(a)
                break
        
        if len(smaller) == 0:
            return "0"

        levels = []

        while smaller:
            number = smaller.pop()
            result = []
            for i in range(len(levels)):
                result.append(0)
            self.multiply2(larger, number, result)
            levels.append(result)
        

        result = self.bulk_add(levels)
        result.reverse()
        return "".join(result)
    
    def multiply2(self, big, m, result):
        carry = 0
        for i in range(len(big)-1,-1,-1):
            a = carry + (big[i] * m)
            result.append(a%10)
            carry = a//10
        if carry:
            result.append(carry)
        return result
    
    def bulk_add(self, levels):
        carry = 0
        levels.reverse()
        i = 0
        result = []
        while levels:
            sm = carry
            for arr in levels:
                sm += arr[i]
            result.append(str(sm%10))
            carry = sm//10
            i+=1
            while levels and i >= len(levels[-1]):
                levels.pop()
        if carry:
            result.append(str(carry))
        return result
```