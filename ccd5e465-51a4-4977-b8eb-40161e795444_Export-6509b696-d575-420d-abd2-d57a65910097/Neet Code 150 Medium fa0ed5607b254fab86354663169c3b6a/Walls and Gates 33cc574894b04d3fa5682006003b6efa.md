# Walls and Gates

Status: Not started
Tags: BFS
Last edited time: November 24, 2023 9:20 PM

[https://leetcode.com/problems/walls-and-gates/](https://leetcode.com/problems/walls-and-gates/)

```python
from collections import deque
class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
        q = deque([])
        for i in range(len(rooms)):
            for j in range(len(rooms[0])):
                if rooms[i][j] == 0:
                    q.append((i,j,0))
        
        while q:
            x,y,distance = q.popleft()
            for a,b in [(0,1), (1,0), (-1,0), (0,-1)]:
                i = a+x
                j = b+y
                if 0 <= i < len(rooms) and 0 <= j < len(rooms[0]) and rooms[i][j] > 0 and distance+1 < rooms[i][j]:
                    rooms[i][j] = distance+1
                    q.append((i, j, distance+1))
```

Idea:

- Naive BFS would reach all node
- If we add all originating points to the queue, we do bi-directional BFS.