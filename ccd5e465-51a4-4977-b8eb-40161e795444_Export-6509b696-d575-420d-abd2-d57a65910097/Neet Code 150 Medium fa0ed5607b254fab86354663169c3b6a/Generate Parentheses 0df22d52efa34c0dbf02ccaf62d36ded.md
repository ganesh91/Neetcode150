# Generate Parentheses

Status: Not started
Tags: DFS, Recursion, Stack
Last edited time: November 29, 2023 11:13 AM

[https://leetcode.com/problems/generate-parentheses/](https://leetcode.com/problems/generate-parentheses/)

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        result = []
        path = []
        self.construct(0, 0, n, path, result)
        return result
    

    def construct(self, start, end, n, path, collector):
        if start == n and end == n:
            collector.append("".join(path))
            return 
        if start < n:
            path.append('(')
            self.construct(start+1, end, n, path, collector)
            path.pop()
        if end < start:
            path.append(')')
            self.construct(start, end+1, n, path, collector)
            path.pop()
```