# Regular Expression Matching

Status: Not started
Tags: Dynamic Programming
Created time: December 19, 2023 6:54 PM

[https://leetcode.com/problems/regular-expression-matching/description/](https://leetcode.com/problems/regular-expression-matching/description/)

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        return self.helper(s,p,0,0)

    @cache
    def helper(self, s, p, i, j):
        if i >= len(s) and j >= len(p):
            return True
        elif j >= len(p):
            return False
        elif i >= len(s) and j+1 < len(p) and p[j+1] == '*':
            return self.helper(s,p,i,j+2)
        elif i >= len(s):
            return False
        elif j+1 < len(p) and p[j+1] == '*':
            if p[j] == '.' or s[i] == p[j]:
                return self.helper(s,p,i+1,j+2) or \
                        self.helper(s,p,i, j+2) or \
                        self.helper(s,p,i+1,j)
            else:
                return self.helper(s,p,i, j+2)
        elif p[j] == '.' or s[i] == p[j]:
            return self.helper(s,p,i+1,j+1)
        else:
            return False
```