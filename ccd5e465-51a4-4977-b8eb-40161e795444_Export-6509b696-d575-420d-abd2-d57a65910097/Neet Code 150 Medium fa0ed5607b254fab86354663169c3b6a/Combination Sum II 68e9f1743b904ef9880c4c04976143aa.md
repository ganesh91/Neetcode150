# Combination Sum II

Status: Not started
Summary: The "Combination Sum II" problem involves finding unique combinations of numbers from a given list that sum up to a target value. The provided Python solution uses recursion and backtracking to generate the combinations, while avoiding duplicates by checking for consecutive identical elements in the list.
Tags: BackTracking
Last edited time: November 23, 2023 3:24 PM

[https://leetcode.com/problems/combination-sum-ii/editorial/](https://leetcode.com/problems/combination-sum-ii/editorial/)

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        collector = []
        candidates.sort()
        print(candidates)
        self.combine(candidates, 0, [], collector, target)
        print(collector)
        return collector
    

    def combine(self, candidates, index, path, collector, target):
        if target == 0:
            collector.append([i for i in path])
            return
        if target < 0:
            return
        for k in range(index, len(candidates)):
            if k == index or (k > index and candidates[k] != candidates[k-1]):
                path.append(candidates[k])
                self.combine(candidates, k+1, path, collector, target-candidates[k])
                path.pop()
```

Logic:

- Normal Super Recursion
- if running sum = target, complete recursion. else cancel recursion and backtrack.
- The case of duplicates is that once its consumed, the next iteration should not consider the same element.
`if k == index or (k > index and candidates[k] != candidates[k-1]):`

is the key to avoid duplicates.