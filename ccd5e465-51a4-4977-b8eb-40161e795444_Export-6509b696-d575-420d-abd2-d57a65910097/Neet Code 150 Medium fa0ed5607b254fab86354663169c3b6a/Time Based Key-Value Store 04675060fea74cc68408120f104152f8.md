# Time Based Key-Value Store

Status: Not started
Tags: Binary Search
Last edited time: November 26, 2023 3:41 PM

[https://leetcode.com/problems/time-based-key-value-store/description/](https://leetcode.com/problems/time-based-key-value-store/description/)

```python
from dataclasses import dataclass

@dataclass
class Entry:
    value: str
    ts: int

class TimeMap:
    def __init__(self):
        self.lookup = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        node = Entry(value, timestamp)
        if key in self.lookup:
            self.lookup[key].append(node)
        else:
            self.lookup[key] = [node]
        

    def get(self, key: str, timestamp: int) -> str:
        if key not in self.lookup:
            return ""
        ts = self.lookup[key]
        return self.bsearch(ts, timestamp)
    
    def bsearch(self, ts, timestamp):
        if ts[0].ts > timestamp:
            return ""
        start, end = 0, len(ts)-1
        while start <= end:
            mid = start + (end-start)//2
            if ts[mid].ts == timestamp:
                return ts[mid].value
            elif ts[mid].ts > timestamp:
                end = mid-1
            else:
                start = mid+1
        
        return ts[end].value

# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)
```