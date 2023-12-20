# Daily Temperatures

Status: Not started
Tags: Stack
Last edited time: November 29, 2023 11:03 AM

[https://leetcode.com/problems/daily-temperatures/](https://leetcode.com/problems/daily-temperatures/)

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        result = [0 for _ in range(len(temperatures))]
        stack = []
        for en,i in enumerate(temperatures):
            while stack and stack[-1][0] < i:
                item = stack.pop()
                result[item[1]] = en-item[1]
            stack.append((i, en))
        return result

    
    # [4,1,2]
```