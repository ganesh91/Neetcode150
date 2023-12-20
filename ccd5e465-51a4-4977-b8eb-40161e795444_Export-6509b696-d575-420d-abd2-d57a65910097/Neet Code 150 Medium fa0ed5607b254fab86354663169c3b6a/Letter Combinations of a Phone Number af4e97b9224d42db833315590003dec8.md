# Letter Combinations of a Phone Number

Status: Not started
Tags: BackTracking
Last edited time: November 26, 2023 3:51 PM

[https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        lookup = {
            '2': ['a','b','c'],
            '3': ['d','e','f'],
            '4': ['g','h','i'],
            '5': ['j','k','l'],
            '6': ['m','n','o'],
            '7': ['p','q','r','s'],
            '8': ['t','u','v'],
            '9': ['w','x','y','z']
        }
        if len(digits) == 0:
            return []
        result = []
        self.recurse(lookup, digits, 0, [], result)
        return result

    
    def recurse(self, lookup, digits, index, stack, result):
        if index >= len(digits):
            result.append("".join(stack))
            return
        for option in lookup[digits[index]]:
            stack.append(option)
            self.recurse(lookup, digits, index+1, stack, result)
            stack.pop()
```