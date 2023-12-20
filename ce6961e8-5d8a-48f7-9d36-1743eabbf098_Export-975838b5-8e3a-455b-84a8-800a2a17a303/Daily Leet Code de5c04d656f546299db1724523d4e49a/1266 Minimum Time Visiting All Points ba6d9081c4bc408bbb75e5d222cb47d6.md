# 1266. Minimum Time Visiting All Points

Status: Not started
Tags: A*, Math

Look at neighbors and select the shortest distance

```python
class Solution:
    def minTimeToVisitAllPoints(self, points: List[List[int]]) -> int:
        distance = 0
        p = 0
        while p+1 < len(points):
            point = points[p]
            target = points[p+1]
            current = point
            while current[0] != target[0] or current[1] != target[1]:
                current = self.getnext(current[0], current[1], target[0], target[1])
                distance += 1
            p+=1
        
        return distance

    def getnext(self, x1, y1, x2, y2):
        neighbors = [(0,1),(1,0),(-1,0), (0,-1), (1,1), (-1,-1), (-1,1), (1,-1)]
        result = []
        for i in neighbors:
            a = x1+i[0]
            b = y1+i[1]
            result.append((((a-x2)**2 + (b-y2)**2)**0.5,[a,b]))
        result.sort()
        return result[0][1]
```

Option 2: Math

```python
class Solution:
    def minTimeToVisitAllPoints(self, points: List[List[int]]) -> int:
        ans = 0
        for i in range(len(points) - 1):
            curr_x, curr_y = points[i]
            target_x, target_y = points[i + 1]
            ans += max(abs(target_x - curr_x), abs(target_y - curr_y))
        
        return ans
```

Idea: The maximum distance to be travelled = max(distance travelled in x or distance travelled in y).