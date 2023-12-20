# Longest Repeating Character Replacement

Status: Not started
Tags: Hash Map, Two Pointers
Last edited time: November 29, 2023 10:47 AM

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        counter = {}
        start, end = 0, 0

        maxlen = 0
        while start < len(s) and end < len(s):
            self.increment(s[end], counter)
            max_occurance, elements = self.max_occurance(counter)
            while elements > max_occurance+k:
                self.decrement(s[start], counter)
                start += 1
                max_occurance, elements = self.max_occurance(counter)
            maxlen = max(maxlen, elements)
            end += 1
        
        return maxlen
        
    
    def increment(self, char, counter):
        if char not in counter:
            counter[char] = 0
        counter[char] += 1
    
    def decrement(self, char, counter):
        if counter[char] == 1:
            del counter[char]
        else:
            counter[char]-=1
    
    def max_occurance(self, counter):
        mx = 0
        sm = 0
        for char in counter:
            mx = max(counter[char], mx)
            sm += counter[char]
        return (mx, sm)
```