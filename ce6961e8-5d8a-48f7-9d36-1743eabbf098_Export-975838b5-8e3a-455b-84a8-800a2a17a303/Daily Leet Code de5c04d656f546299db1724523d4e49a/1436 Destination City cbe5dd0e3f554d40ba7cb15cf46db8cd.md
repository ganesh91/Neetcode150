# 1436. Destination City

Status: Not started
Tags: DFS

```jsx
class Solution:
    def destCity(self, paths: List[List[str]]) -> str:
        cities = set([])
        origins = set([])
        for source, destination in paths:
            cities.add(source)
            cities.add(destination)
            origins.add(source)
        
        for city in cities:
            if city not in origins:
                return city
        
        return ""
```