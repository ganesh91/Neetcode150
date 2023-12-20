# 2353. Design a Food Rating System

Status: Not started
Tags: Hash Map, Heap

[https://leetcode.com/problems/design-a-food-rating-system/description/](https://leetcode.com/problems/design-a-food-rating-system/description/)

```python
from dataclasses import dataclass, field
import heapq

@dataclass(order=True)
class Rating:
    rating: int
    food: str
    cuisine: str = field(compare=False)
    tombstone: bool = field(compare=True, default=False)

    def updateRating(self, rating):
        self.tombstone = True
        return Rating(-rating, self.food, self.cuisine)

class FoodRatings:

    def __init__(self, foods: List[str], cuisines: List[str], ratings: List[int]):
        self._food_lookup = {}
        self._cuisine_lookup = defaultdict(list)
        for i in range(len(foods)):
            food_name = foods[i]
            cuisine_name = cuisines[i]
            rating = ratings[i]
            item = Rating(-rating, food_name, cuisine_name)
            self._food_lookup[food_name] = item
            self._cuisine_lookup[cuisine_name].append(item)
        for i in self._cuisine_lookup:
            heapq.heapify(self._cuisine_lookup[i])

        

    def changeRating(self, food: str, newRating: int) -> None:
        item = self._food_lookup[food].updateRating(newRating)
        self._food_lookup[food] = item
        heapq.heappush(self._cuisine_lookup[item.cuisine], item)
        

    def highestRated(self, cuisine: str) -> str:
        while self._cuisine_lookup[cuisine] and self._cuisine_lookup[cuisine][0].tombstone:
            heapq.heappop(self._cuisine_lookup[cuisine])
        return self._cuisine_lookup[cuisine][0].food
        

# Your FoodRatings object will be instantiated and called as such:
# obj = FoodRatings(foods, cuisines, ratings)
# obj.changeRating(food,newRating)
# param_2 = obj.highestRated(cuisine)
```