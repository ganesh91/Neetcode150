# 242. Valid Anagram

Status: Not started
Tags: Two Pointer

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        lookup = [0 for _ in range(26)]
        begin = ord('a')
        for i in s:
            lookup[ord(i)-begin]+=1
        for i in t:
            if lookup[ord(i)-begin] > 0:
                lookup[ord(i)-begin]-=1
            else:
                return False
        return sum(lookup) == 0
```