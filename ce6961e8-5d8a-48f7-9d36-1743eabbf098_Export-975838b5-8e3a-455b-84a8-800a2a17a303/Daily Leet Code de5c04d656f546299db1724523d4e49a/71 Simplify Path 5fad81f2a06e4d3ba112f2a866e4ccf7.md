# 71. Simplify Path

Status: Not started
Tags: Stack

[https://leetcode.com/problems/simplify-path/](https://leetcode.com/problems/simplify-path/)

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        paths = path.split("/")
        result = []
        for i in paths:
            if i == '' or i == '.':
                pass
            elif i == '..':
                if len(result) > 0:
                    result.pop()
            else:
                result.append(i)
        return "/"+"/".join(result)
```