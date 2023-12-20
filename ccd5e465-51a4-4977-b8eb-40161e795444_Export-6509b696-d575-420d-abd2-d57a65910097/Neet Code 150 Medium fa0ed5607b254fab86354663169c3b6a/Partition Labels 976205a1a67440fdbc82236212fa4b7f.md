# Partition Labels

Status: Not started
Tags: Greedy, Two Pointers
Last edited time: December 3, 2023 6:28 PM

[https://leetcode.com/problems/partition-labels/](https://leetcode.com/problems/partition-labels/)

```python
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        lookup = {}
        for en,i in enumerate(s):
            lookup[i] = en
        partitions = []
        
        start = 0
        end = lookup[s[start]]
        current = 0

        while current < len(s):
            if end < current:
                partitions.append(current-start)
                start = current
            end = max(end, lookup[s[current]])
            current += 1
        partitions.append(current-start)
        
        
        return partitions
```