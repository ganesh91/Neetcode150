# Meeting Rooms II

Status: Not started
Summary: This document provides a Python solution for the "Meeting Rooms II" problem. The solution uses a priority queue to keep track of meeting end times and determines the minimum number of meeting rooms required.
Tags: Heap
Last edited time: November 23, 2023 3:27 PM

Version 1

```python
import heapq
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        intervals.sort(key = lambda x: x[0])
        q = []
        minRooms = 0
        for i in intervals:
            while q and q[0][0] <= i[0]:
                heapq.heappop(q)
            heapq.heappush(q, (i[1], i[0]))
            minRooms = max(minRooms, len(q))
        return minRooms
```