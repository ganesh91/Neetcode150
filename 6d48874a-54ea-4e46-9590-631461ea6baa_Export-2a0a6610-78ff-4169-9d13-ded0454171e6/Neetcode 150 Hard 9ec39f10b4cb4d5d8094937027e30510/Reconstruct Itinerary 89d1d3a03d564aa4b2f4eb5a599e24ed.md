# Reconstruct Itinerary

Status: Not started
Tags: Graph
Created time: December 20, 2023 2:02 PM

[https://leetcode.com/problems/reconstruct-itinerary/description/](https://leetcode.com/problems/reconstruct-itinerary/description/)

Backtracking

```python
from collections import deque
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        graph = {}
        for cities in tickets:
            source, dest = cities
            if source in graph:
                graph[source].append(dest)
            else:
                graph[source] = [dest]
        
        bitmap = {}

        for j in graph:
            graph[j].sort()
            bitmap[j] = [False for _ in range(len(graph[j]))]
        
        itin = []
        itin.append("JFK")
        return self.journey(graph, bitmap, itin, "JFK", len(tickets))
        
    
    def journey(self, graph, visited, itin, prev, tickets):
        longest = []
        nxt = graph[prev] if prev in graph else []
        for en, destination in enumerate(nxt):
            if not visited[prev][en] and len(longest) == 0:
                itin.append(destination)
                visited[prev][en] = True
                plan = self.journey(graph, visited, itin, destination, tickets)
                visited[prev][en] = False
                itin.pop()
                longest = longest if len(longest) >= len(plan) else plan
        if len(itin) == tickets+1:
            longest = itin[:]
        return longest
```

Version 2: Visit once

since there is a guarantee, a node exists, this works.

```python
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        graph = {}
        for source, destination in tickets:
            if source not in graph:
                graph[source] = []
            graph[source].append(destination)
        
        for source in graph:
            graph[source].sort(reverse=True)
        
        path = []
        self.travel("JFK", path, graph)
        path.reverse()

        return path
    
    def travel(self, source, path, graph):
        destinations = graph[source] if source in graph else []
        while destinations:
            nxt = destinations.pop()
            self.travel(nxt, path, graph)
        path.append(source)
```