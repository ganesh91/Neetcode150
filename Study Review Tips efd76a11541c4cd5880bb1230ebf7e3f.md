# Study Review Tips

## Binary & Bitwise Operations

| Operation | Result |
| --- | --- |
| op1 & op2 | Operator 1 ANDS operator 2 |
| op1 | op2 | Operator 1 OR operator 2 |
| ~ op | NOTs operator |
| ^ | XORs operator |
| << |  Left shift Operator |
|  << 1 | Multiplies by two |
| >> | Right shift operator |
| >> 1 | Divides by 2 |

## All Shortest Paths

- [https://en.wikipedia.org/wiki/Floyd–Warshall_algorithm](https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm)

$$

  
    
      
        
          m
          i
          n
        
        
          
            (
          
        
        
          s
          h
          o
          r
          t
          e
          s
          t
          P
          a
          t
          h
        
        (
        i
        ,
        j
        ,
        k
        −
        1
        )
        ,
      
    
    
  

  
    
      
        
          s
          h
          o
          r
          t
          e
          s
          t
          P
          a
          t
          h
        
        (
        i
        ,
        k
        ,
        k
        −
        1
        )
        +
        
          s
          h
          o
          r
          t
          e
          s
          t
          P
          a
          t
          h
        
        (
        k
        ,
        j
        ,
        k
        −
        1
        )
        
          
            )
          
        
      
    
    
  
.
$$

```python
for start in range(nodes):
	for destination in range(nodes):
		for intermediary in range(nodes):
			dp[start][destination] = min(dp[start][destination], dp[start][intermediary]+dp[intermediary][destination]
```

## Dikstra’s Algorithm vs BFS

- BFS, edges are entered in queue
- Diksta’s, vertices are entered in queue

BFS:

```python
while q:
	node = q.popleft()
	for neighbors in graph[node]:
		q.append(neighbors, node.distance+distance_to_neighbor)
```

DFS:

```python
heap = []
heap.append((start_node,0))

node_distance_so_far = defaultdict(inf)

while heap:
	node = heapq.heappop(heap)
	node_distance_so_far[node] = node.distance # We have visited the node.
	#Dikstra's greedy criterion: for any non-neg node, the first time we visit is shortest
	for neigbors:
		if not visited:
			add to heap
	heapify queue
```

Implementations: [[743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)](https://www.notion.so/743-Network-Delay-Time-8d5612add3aa459d97a62866fcce759b?pvs=21) 

## Bellman Ford

Iterate through all possibilities from jumping to one vertex at a time from origin node.

Similar to DP

```python
initialize distance from all nodes to source node to zero
distance[src -> src] = 0

while node < len(nodes):
	distance[i] = min(distance[i], min(distance to i from all predecessors+distance)
```

```python
while k >= 0:
   k-=1
   current_dp = dp[:]
   for source in graph:
       for dest in graph[source]:
            current_dp[dest] = min(current_dp[dest], dp[source]+graph[source][dest])
            dp = current_dp
```

## Kruskal - Minimum spanning tree

```python
- Initialize Union-Find
- add neighbors to heap
- extract heap-min
	- if edge connects different roots, union(v1,v2)
	- else disregard
```