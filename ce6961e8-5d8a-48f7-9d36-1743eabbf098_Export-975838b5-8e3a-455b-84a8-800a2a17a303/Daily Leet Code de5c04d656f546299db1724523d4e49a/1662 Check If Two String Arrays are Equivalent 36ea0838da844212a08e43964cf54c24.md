# 1662. Check If Two String Arrays are Equivalent

Status: Not started
Tags: Two Pointer

[https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent/](https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent/)

```python
class Iterator:
    def __init__(self, iterable):
        self.iterable = iterable
        self.size = len(self.iterable)
        self.cw = 0
        self.ci = 0
    
    def __next__(self):
        if self.cw < self.size:
            if self.ci < len(self.iterable[self.cw]):
                val =  self.iterable[self.cw][self.ci]
                self.ci += 1
                return val
            else:
                self.ci = 0
                self.cw += 1
                return next(self)
        else:
            return None

class Solution:
    def arrayStringsAreEqual(self, word1: List[str], word2: List[str]) -> bool:
        i1 = Iterator(word1)
        i2 = Iterator(word2)

        p1, p2 = next(i1), next(i2)
        while p1 and p2 and p1 == p2:
            p1, p2 = next(i1), next(i2)
        
        return p1 == p2
```