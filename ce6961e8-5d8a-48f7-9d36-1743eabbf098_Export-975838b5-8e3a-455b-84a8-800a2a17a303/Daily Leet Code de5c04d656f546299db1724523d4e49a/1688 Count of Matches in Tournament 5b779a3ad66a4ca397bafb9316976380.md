# 1688. Count of Matches in Tournament

Status: Not started
Tags: Recursion

[https://leetcode.com/problems/count-of-matches-in-tournament/](https://leetcode.com/problems/count-of-matches-in-tournament/)

```python
class Solution:
    def numberOfMatches(self, n: int) -> int:
        if n <= 1:
            return 0
        elif n % 2 == 0:
            return n//2 + self.numberOfMatches(n//2)
        else:
            return (n-1)//2 + self.numberOfMatches(((n-1)//2)+1)
```