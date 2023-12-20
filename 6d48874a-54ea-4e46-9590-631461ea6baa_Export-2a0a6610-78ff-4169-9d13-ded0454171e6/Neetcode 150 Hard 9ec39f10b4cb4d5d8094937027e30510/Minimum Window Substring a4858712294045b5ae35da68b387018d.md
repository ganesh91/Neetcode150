# Minimum Window Substring

Status: Not started
Tags: Two Pointers
Created time: December 16, 2023 2:10 PM

[https://leetcode.com/problems/minimum-window-substring/](https://leetcode.com/problems/minimum-window-substring/)

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        unique_chars = len(set(t))
        target_chars = {}
        
        for c in t:
            if c not in target_chars:
                target_chars[c] = 0
            target_chars[c] += 1
        
        min_len, min_str = float('inf'), ""

        start, current = 0,0
        
        complete_chars, current_chars = 0, {}
        
        for i in target_chars:
            current_chars[i] = 0

        while current < len(s):
            char = s[current]
            if char in target_chars:
                current_chars[char] += 1
                if current_chars[char] == target_chars[char]:
                    complete_chars += 1
                if complete_chars == unique_chars:
                    start = self.contract(s, start, current_chars, target_chars)
                    if current-start < min_len:
                        min_len = current-start
                        min_str = s[start:current+1]
                    start += 1
                    complete_chars -= 1
            current += 1
        
        return min_str
    
    def contract(self,s, start, current, lookup):
        while True:
            char = s[start]
            if char not in lookup:
                start += 1
            elif current[char] > lookup[char]:
                start+=1
                current[char] -= 1
            else:
                current[char] -= 1
                break
        return start
```