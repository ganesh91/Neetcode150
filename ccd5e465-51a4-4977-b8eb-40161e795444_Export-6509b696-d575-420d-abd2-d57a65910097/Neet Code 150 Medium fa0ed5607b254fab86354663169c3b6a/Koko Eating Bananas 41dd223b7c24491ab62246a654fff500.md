# Koko Eating Bananas

Status: Not started
Summary: The "Koko Eating Bananas" problem on LeetCode is solved using binary search on the k-space. The provided Python code implements the solution, where the minimum eating speed is determined by iterating through the piles and checking if the total time is less than or equal to the given hours.
Tags: Binary Search
Last edited time: November 24, 2023 11:01 AM

[https://leetcode.com/problems/koko-eating-bananas/](https://leetcode.com/problems/koko-eating-bananas/)

Idea:

- Binary search on k-space rather than the input array space.

```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        start = 1
        end = max(piles)
        while start < end:
            mid = start+ (end-start)//2
            if self.consume(piles, h, mid):
                end = mid
            else:
                start = mid+1
        return start
    
    def consume(self, piles, h, k):
        time = 0
        for i in piles:
            if i % k == 0:
                time += i//k
            else:
                time += (i//k) + 1
        return time <= h
```