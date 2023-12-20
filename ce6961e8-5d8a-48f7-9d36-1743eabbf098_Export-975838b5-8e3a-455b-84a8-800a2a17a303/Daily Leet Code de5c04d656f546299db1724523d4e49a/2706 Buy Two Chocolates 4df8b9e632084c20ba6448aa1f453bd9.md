# 2706. Buy Two Chocolates

Status: Not started
Tags: Sorting

```python
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        first_min = float('inf')
        second_min = float('inf')

        for i in prices:
            if i <= first_min:
                second_min = first_min
                first_min = i
            else:
                second_min = min(second_min, i)

        if first_min + second_min <= money:
            money -= first_min + second_min
        
        return money
```