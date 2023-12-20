# Course Schedule II

Status: Not started
Tags: DFS, Graph
Last edited time: November 25, 2023 1:48 PM

[https://leetcode.com/problems/course-schedule-ii/editorial/](https://leetcode.com/problems/course-schedule-ii/editorial/)

```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        course_graph = {}
        for course, prereq in prerequisites:
            if course in course_graph:
                course_graph[course].append(prereq)
            else:
                course_graph[course]=[prereq]
        
        course_taken = set([])
        result = []
        visited = set([])
        for course in range(numCourses):
            if not self.study(course_graph, course, visited, course_taken, result):
                return []
        return result
        
    
    def study(self, course_graph, course, current_seq, course_taken, result):
        if course in course_taken:
            return True
        if course in current_seq:
            return False
        current_seq.add(course)
        if course not in course_graph:
            course_taken.add(course)
            result.append(course)
            return True
        can_complete = True
        for prereq in course_graph[course]:
            can_complete = can_complete and self.study(course_graph, prereq, current_seq, course_taken, result)
            if not can_complete:
                return can_complete
        course_taken.add(course)
        result.append(course)
        return can_complete
```