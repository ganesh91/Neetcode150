# Cheapest Flights with K Stops

Status: Not started
Tags: Graph
Last edited time: December 20, 2023 8:53 PM

[https://leetcode.com/problems/cheapest-flights-within-k-stops/](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

```python
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, k: int) -> int:
        graph = {}
        for source, dest, distance in flights:
            if source not in graph:
                graph[source] = {}
            graph[source][dest] = distance
        
        dp = [float('inf') for i in range(n)]
        dp[src] = 0

        while k >= 0:
            k-=1
            current_dp = dp[:]
            for source in graph:
                for dest in graph[source]:
                    current_dp[dest] = min(current_dp[dest], dp[source]+graph[source][dest])
            dp = current_dp

        val = dp[dst]
        return val if val < float('inf') else -1
```