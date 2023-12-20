# Course Schedule

Status: Not started
Tags: DFS, Topological Sort
Last edited time: November 29, 2023 6:39 PM

[https://leetcode.com/problems/course-schedule/](https://leetcode.com/problems/course-schedule/)

```python
from collections import defaultdict
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        completed_courses = set([])
        
        graph = {}
        for course,prereq in prerequisites:
            if course in graph:
                graph[course].append(prereq)
            else:
                graph[course] = [prereq]
        
        for i in range(numCourses):
            if i not in completed_courses:
                current_course = set([])
                val = self.study(i, graph, current_course, completed_courses)
                print(i, val)
                if not val:
                    return False
        
        return True
    
    def study(self, course, graph, current, completed):
        if course not in graph or course in completed:
            return True
        if course in current:
            return False
        canComplete = True
        current.add(course)
        for prereq in graph[course]:
            canComplete = canComplete and self.study(prereq, graph, current, completed)
            if not canComplete:
                break
        completed.add(course)
        return canComplete
```