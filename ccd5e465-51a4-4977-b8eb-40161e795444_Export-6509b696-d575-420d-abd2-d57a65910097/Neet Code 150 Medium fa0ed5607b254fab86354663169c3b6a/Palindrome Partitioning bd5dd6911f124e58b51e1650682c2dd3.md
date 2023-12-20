# Palindrome Partitioning

Status: Not started
Tags: BackTracking, Dynamic Programming
Last edited time: November 27, 2023 1:42 PM

[https://leetcode.com/problems/palindrome-partitioning/description/](https://leetcode.com/problems/palindrome-partitioning/description/)

Idea:

- Notice if “abba” is a palindrome, “bb” is also a palindrome
- Start from a starting point, from the farthest, find which end point makes it palindrome
- if say 0,4 is palindrome, (1,3), (2,2) is a palindrome
- Populate this in the dp table

- While backtracking to re-construct the vectors
    - if dp[start][end] = false, include current element
    - if dp[start][end] = true, include slice
    - Reconstruct the array and continue

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        dp = [[False for _ in range(len(s))] for _ in range(len(s))]
        for start in range(len(s)):
            for end in range(len(s)-1, -1,-1):
                if not dp[start][end] and self.isPalindrome(s, start, end):
                    a,b = start, end
                    while b >= a:
                        dp[a][b] = True
                        a+= 1
                        b-= 1
        for i in dp:
            print(i)
        collector = []
        self.backtrack(dp, s, 0, [], collector)
        return collector
    
    def backtrack(self, board, s, i, path, collector):
        if i >= len(s):
            collector.append([i for i in path])
            return
        for j in range(i, len(s)):
            if j == i or board[i][j]:
                path.append(s[i:j+1])
                self.backtrack(board, s, j+1, path, collector)
                path.pop()
    
    def isPalindrome(self, s, start, end):
        while start < end:
            if s[start] != s[end]:
                return False
            else:
                start += 1
                end -=1
        return True
```