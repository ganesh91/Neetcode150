# Valid Palindrome

Status: Not started
Tags: Two Pointer

[https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        start, end = 0, len(s)-1
        accept = set(i for i in 'abcdefghijklmnopqrstuvwxyz01234567890')
        while start < end:
            if s[start].lower() not in accept:
                start+=1
            elif s[end].lower() not in accept:
                end-=1
            elif s[start].lower() == s[end].lower():
                start+=1
                end-=1
            else:
                return False
        return True
```