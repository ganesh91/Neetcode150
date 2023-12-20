# Combination Sum

Status: Not started
Tags: BackTracking
Last edited time: November 27, 2023 10:45 AM

[https://leetcode.com/problems/combination-sum/description/](https://leetcode.com/problems/combination-sum/description/)

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        collector = []
        self.assemble(candidates, 0, target, [], collector)
        return collector
    
    def assemble(self, candidates, begin, target, path, collector):
        if target == 0:
            collector.append([i for i in path])
            return
        if target < 0:
            return
        for i in range(begin, len(candidates)):
            num = candidates[i]
            path.append(num)
            self.assemble(candidates, i, target-num, path, collector)
            path.pop()
```