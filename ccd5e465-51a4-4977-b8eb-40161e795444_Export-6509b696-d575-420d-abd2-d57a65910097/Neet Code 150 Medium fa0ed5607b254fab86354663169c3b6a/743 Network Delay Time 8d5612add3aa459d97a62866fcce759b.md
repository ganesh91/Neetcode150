# 743. Network Delay Time

Status: Not started
Tags: Graph
Last edited time: December 16, 2023 1:28 PM

Version 1:

All out BFS

```python
from collections import deque
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        distance = [float('inf') for i in range(n+1)]
        distance[k] = 0
        distance[0] = 0
        
        q = deque([])
        q.append((k, 0))

        graph = {}
        for source, target, dist in times:
            if source not in graph:
                graph[source] = {}
            if target not in graph[source]:
                graph[source][target] = dist
        

        while q:
            node, dist_so_far = q.popleft()
            if node in graph:
                for child in graph[node]:
                    dist = dist_so_far + graph[node][child]
                    if distance[child] > dist:
                        distance[child] = dist
                        q.append((child, dist))
        
        print(distance)
        distance.sort()
        return -1 if distance[-1] == float('inf') else distance[-1]
```

Version 2:

Dikastra’s Algorithm

```python
import heapq
from dataclasses import dataclass, field

@dataclass(order=True)
class Distance:
    node: int = field(compare=False)
    distance: int

class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        distances = [float(inf) for i in range(n+1)]
        distances[0] = 0

        graph = {}
        for source, target, dist in times:
            if source not in graph:
                graph[source] = {}
            if target not in graph[source]:
                graph[source][target] = dist
        
        q = []
        q.append(Distance(k,0))

        nodes_in_heap = {}
        
        while q:
            shortest = heapq.heappop(q)
            distances[shortest.node] = shortest.distance
            if shortest.node in graph:
                for child in graph[shortest.node]:
                    if distances[child] == float('inf'):
                        # This means I have not visited the node
                        if child in nodes_in_heap:
                            nodes_in_heap[child].distance = min(nodes_in_heap[child].distance, shortest.distance+graph[shortest.node][child])
                        else:
                            c_next = Distance(child, shortest.distance+graph[shortest.node][child])
                            nodes_in_heap[child] = c_next
                            q.append(c_next)
                heapq.heapify(q)
        
        print(distances)
        distances.sort()
        return -1 if distances[-1] == float('inf') else distances[-1]
```