# 2957. Remove Adjacent Almost-Equal Characters

Status: Not started
Tags: Dynamic Programming

```python
class Solution:
    def removeAlmostEqualCharacters(self, word: str) -> int:
        return self.replace(word, 0)
    
    @cache
    def replace(self, word, index):
        if index >= len(word):
            return 0
        if index + 1 < len(word) and self.is_approx(word[index], word[index+1]):
            return min(self.replace(word, index+2), self.replace(word, index+1))+1
        else:
            return self.replace(word, index+1)
    
    def is_approx(self, a, b):
        return abs(ord(a)-ord(b)) <= 1
```