# 2391. Minimum Amount of Time to Collect Garbage

Status: Not started
Tags: Prefix Sum, Preprocessing

[https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage/](https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage/)

```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        prefix_sum = []
        for i in travel:
            if len(prefix_sum) == 0:
                prefix_sum.append(i)
            else:
                prefix_sum.append(prefix_sum[-1]+i)
        
        total_garbages = {'M':0, 'P':0, 'G':0}
        max_index = {'M':0, 'P':0, 'G':0}

        for en,i in enumerate(garbage):
            for c in i:
                total_garbages[c]+=1
                max_index[c] = en
        
        min_duration = 0
        for i in total_garbages:
            pickup_duration = total_garbages[i]
            travel_duration = 0 if max_index[i] == 0 else prefix_sum[max_index[i]-1]
            print(i, pickup_duration, travel_duration)
            min_duration += (pickup_duration + travel_duration)
        
        return min_duration
```