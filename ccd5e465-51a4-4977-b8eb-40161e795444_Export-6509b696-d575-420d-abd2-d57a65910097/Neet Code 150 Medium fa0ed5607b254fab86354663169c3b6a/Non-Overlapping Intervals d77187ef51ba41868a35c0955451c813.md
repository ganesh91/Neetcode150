# Non-Overlapping Intervals

Status: Not started
Summary: The document provides three versions of a solution for the "Non-Overlapping Intervals" problem. The first version uses a recursive approach, the second version optimizes the recursion by skipping overlapping intervals, and the third version uses binary search to find the next non-overlapping interval.
Tags: Dynamic Programming
Last edited time: November 23, 2023 3:26 PM

Version 1.0

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key = lambda x: x[0])
        cache = [-1 for i in range(len(intervals))]
        for i in range(len(intervals)):
            self.choice(i, intervals, cache)
        print(intervals)
        print(cache)
        return len(intervals)-max(cache)

    def choice(self, i, intervals, cache):
        if cache[i] >= 0:
            return cache[i]
        max_intervals = 1
        for j in range(i+1, len(intervals)):
            if not (intervals[i][0] <= intervals[j][0] < intervals[i][1]):
                max_intervals = max(max_intervals, self.choice(j, intervals, cache)+1)
        cache[i] = max_intervals
        return max_intervals
```

Similar to word break, for every interval, check the next interval does not have overlap and include it in the current count

Logic 2:

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key = lambda x: x[0])
        cache = [-1 for i in range(len(intervals))]
        for i in range(len(intervals)):
            self.choice(i, intervals, cache)
        print(intervals)
        print(cache)
        return len(intervals)-max(cache)

    def choice(self, i, intervals, cache):
        if i >= len(intervals):
            return 0
        if cache[i] >= 0:
            return cache[i]
        max_intervals = 1
        for j in range(i+1, len(intervals)):
            if not (intervals[i][0] <= intervals[j][0] < intervals[i][1]):
                max_intervals = max(max_intervals, self.choice(j, intervals, cache)+1)
                # Once I have the next overlap
                break
        max_intervals = max(max_intervals, self.choice(i+1, intervals, cache))
        cache[i] = max_intervals
        return max_intervals
```

Rather than iterating, through everything, keep the next choice and skip in the same dp

Variant 3:

Rather than iterating and finding the next non-overlap, binary search and find.

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort()
        
        @lru_cache(None)
        def dp(idx):
            if idx == len(intervals):
                return 0
            start, end = intervals[idx]
            # drop this?
            next_dp = dp(idx+1)
            # keep this?
            jump_idx = bisect.bisect_right(intervals, [end, float('-inf')])
            
            ans = max(next_dp, dp(jump_idx)+1)
            return ans
       
        return len(intervals) - dp(0)
```