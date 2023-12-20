# Longest Palindroming Substring

Status: Not started
Tags: Dynamic Programming
Last edited time: November 30, 2023 2:56 PM

Idea:

- Expand from middle

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        max_string = ""

        for i in range(len(s)):
            (start,end) = self.expand(s, i, i)
            if end-start > len(max_string):
                max_string = s[start: end]
            
            (start, end) = self.expand(s, i, i+1)
            if end-start > len(max_string):
                max_string = s[start: end]
        
        return max_string
    

    def expand(self, s, start, end):
        while start >=0 and end < len(s) and s[start] == s[end]:
            start -= 1
            end += 1
        return (start+1, end)
```