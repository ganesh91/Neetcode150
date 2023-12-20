# Alien Dictionary

Status: Not started
Tags: Topological Sort
Created time: December 20, 2023 7:27 PM

[https://leetcode.com/problems/alien-dictionary/](https://leetcode.com/problems/alien-dictionary/)

```python
class Solution:
    def alienOrder(self, words: List[str]) -> str:
        graph = {}
        unique_letters = set([])

        for i in range(len(words)-1):
            if words[i] == words[i+1]:
                continue
            smaller, larger = self.get_relation(words[i], words[i+1])
            if smaller == None:
                return ""
            if smaller not in graph:
                graph[smaller] = []
            if larger not in graph[smaller]:
                graph[smaller].append(larger)
            
        for word in words:
            for c in word:
                unique_letters.add(c)
        
        g_visited = set([])
        order = []
        for source in unique_letters:
            if source not in g_visited:
                l_visited = set([])
                has_cycle = self.jump(source, l_visited, g_visited, graph, order)
                if has_cycle:
                    return ""
                g_visited.update(l_visited)
        
        order.reverse()
        return "".join(order)
    
    def jump(self, source, l_visited, g_visited, graph, order):
        l_visited.add(source)
        has_cycle = False
        if source in graph:
            for destination in graph[source]:
                has_cycle = has_cycle or destination in l_visited
                if has_cycle:
                    break
                if destination in g_visited:
                    continue
                has_cycle = has_cycle or self.jump(destination, l_visited, g_visited, graph, order)
        else:
            g_visited.add(source)
        order.append(source)
        return has_cycle
            
    
    def get_relation(self, word1, word2):
        i = 0
        while i < len(word1):
            if i < len(word2):
                if word1[i] != word2[i]:
                    return (word1[i], word2[i])
            i+=1
        if len(word1) < len(word2):
            return (word1, word1)
        return (None, None)
```