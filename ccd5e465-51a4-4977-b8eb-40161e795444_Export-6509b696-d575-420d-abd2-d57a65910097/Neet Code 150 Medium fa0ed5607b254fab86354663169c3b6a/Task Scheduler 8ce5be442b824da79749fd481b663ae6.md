# Task Scheduler

Status: Not started
Tags: Heap
Last edited time: November 28, 2023 7:10 PM

[https://leetcode.com/problems/task-scheduler/](https://leetcode.com/problems/task-scheduler/)

```python
from dataclasses import dataclass, field
import heapq
from collections import defaultdict

@dataclass(order=True)
class WorkUnit:
    task: str = field(compare=False)
    priority: int

class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        task_clock = defaultdict(lambda: -n)
        q = []
        for task in tasks:
            heapq.heappush(q, WorkUnit(task, task_clock[task]+n))
            task_clock[task] += n+1
        
        duration = 0
        while q:
            task = heapq.heappop(q)
            print(f"processing {task} at duration {duration}")
            if task.priority <= duration:
                duration += 1
            else:
                duration += (task.priority - duration) + 1
        
        return duration
```