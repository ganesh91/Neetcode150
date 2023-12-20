# Permutation in String

Status: Not started
Tags: Sliding Window, Two Pointers
Last edited time: November 28, 2023 7:42 PM

[https://leetcode.com/problems/permutation-in-string/](https://leetcode.com/problems/permutation-in-string/)

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        lookup = {}
        for i in s1:
            if i not in lookup:
                lookup[i] = 1
            else:
                lookup[i] += 1
        
        spread = len(s1)

        start = 0
        current = 0
        matched = 0
        while current < len(s2):
            # print(current, lookup, start, s2[current])
            if s2[current] not in lookup:
                if current == start:
                    current += 1
                    start += 1
                else:
                    #start rolling
                    while start < current:
                        lookup[s2[start]] += 1
                        matched -= 1
                        start += 1
            elif s2[current] in lookup and lookup[s2[current]] > 0:
                lookup[s2[current]] -= 1
                matched += 1
                current += 1
            elif start < current:
                lookup[s2[start]] += 1
                matched -= 1
                start += 1
            
            if matched == len(s1):
                return True
        
        return matched == len(s1)
```