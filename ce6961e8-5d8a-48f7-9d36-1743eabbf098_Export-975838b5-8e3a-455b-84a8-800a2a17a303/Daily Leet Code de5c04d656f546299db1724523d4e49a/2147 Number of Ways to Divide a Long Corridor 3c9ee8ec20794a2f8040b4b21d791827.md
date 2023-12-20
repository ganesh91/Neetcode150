# 2147. Number of Ways to Divide a Long Corridor

Status: Not started
Tags: Preprocessing, Recursion

[https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor/](https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor/)

```python
class Solution:
    def numberOfWays(self, corridor: str) -> int:
        if len(corridor) == 0:
            return 0
        seats = []
        plants = []
        cp = 1
        for i in corridor:
            if i == 'S':
                seats.append(i)
                plants.append(cp)
                cp = 1
            else:
                cp += 1
        
        if len(seats) == 0 or len(seats) % 2 != 0:
            return 0
        
        plants[0] = 1
        
        return self.recurse(seats, plants, 0) % (10**9 + 7)
    
    def recurse(self, seats, plants, index):
        if index >= len(seats):
            return 1
        return plants[index]*self.recurse(seats, plants, index+2)
```