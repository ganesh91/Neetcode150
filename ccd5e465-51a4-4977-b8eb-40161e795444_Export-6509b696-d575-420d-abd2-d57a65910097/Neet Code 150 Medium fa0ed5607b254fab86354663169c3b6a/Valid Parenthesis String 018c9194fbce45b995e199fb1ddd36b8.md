# Valid Parenthesis String

Status: Not started
Tags: Dynamic Programming
Last edited time: December 3, 2023 2:54 PM

[https://leetcode.com/problems/valid-parenthesis-string/](https://leetcode.com/problems/valid-parenthesis-string/)

```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        choices = [[None for i in range(len(s)+1)] for j in range(len(s)+1)]
        return self.check(0,0,0,s, choices)
    
    def check(self, opens, closes, i, s, choices):
        if i >= len(s):
            return opens == closes
        if closes > opens:
            return False
        if choices[i][opens-closes] is not None:
            return choices[i][opens-closes]
        result = None
        if s[i] == '(':
            result =  self.check(opens+1, closes, i+1, s, choices)
        elif s[i] == ')':
            result =  self.check(opens, closes+1, i+1, s, choices)
        else:
            result = self.check(opens+1, closes, i+1, s, choices) or \
                    self.check(opens, closes+1, i+1, s, choices) or \
                    self.check(opens, closes, i+1, s, choices)
        choices[i][opens-closes] = result
        return result
```