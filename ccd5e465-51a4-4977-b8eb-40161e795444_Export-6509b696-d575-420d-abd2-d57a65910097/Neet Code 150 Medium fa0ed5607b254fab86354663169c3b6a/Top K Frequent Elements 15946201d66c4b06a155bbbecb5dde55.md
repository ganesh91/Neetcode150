# Top K Frequent Elements

Status: Not started
Summary: The document provides a Python solution for the problem "Top K Frequent Elements" on LeetCode. The solution uses a counter to count the frequency of each element in the given list, and then uses a heap to maintain the top k frequent elements. The final result is a list of the top k frequent elements.
Tags: Heap
Last edited time: November 23, 2023 3:26 PM

[https://leetcode.com/problems/top-k-frequent-elements/](https://leetcode.com/problems/top-k-frequent-elements/)

```python
import heapq
from dataclasses import dataclass, field

@dataclass(order=True)
class Container:
    num: int = field(compare=False)
    freq: int

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = {}
        for i in nums:
            if i in counter:
                counter[i] += 1
            else:
                counter[i] = 1
        
        q = []

        for i in counter:
            if len(q) < k:
                heapq.heappush(q, Container(i, counter[i]))
            else:
                heapq.heappushpop(q, Container(i, counter[i]))
        
        return [i.num for i in q]
```