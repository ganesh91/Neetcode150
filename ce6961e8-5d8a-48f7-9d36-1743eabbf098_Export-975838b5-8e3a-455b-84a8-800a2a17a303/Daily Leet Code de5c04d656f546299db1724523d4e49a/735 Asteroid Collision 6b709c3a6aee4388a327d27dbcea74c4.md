# 735. Asteroid Collision

Status: Not started
Tags: Stack

[https://leetcode.com/problems/asteroid-collision/](https://leetcode.com/problems/asteroid-collision/)

Code:

```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        asteroids = [(i, i<0) for i in asteroids]
        result = []
        while asteroids:
            if result and result[-1][1] and not asteroids[-1][1]:
                asteroids.append(result.pop())
            elif len(asteroids) > 1 and asteroids[-1][1] and not asteroids[-2][1]:
                left = asteroids.pop()
                right = asteroids.pop()
                if abs(left[0]) < abs(right[0]):
                    asteroids.append(right)
                elif abs(right[0]) < abs(left[0]):
                    asteroids.append(left)
            else:
                result.append(asteroids.pop())
        return reversed([i[0] for i in result])
```

Modification:

Second question is a similar to first question but when two asteroids with same size collide (i.e when the one with negative sign collides with positive sign) instead of canceling each other out( like in first question) they change the direction and move in opposite directions (positive one now becomes negative and moves back and negative one become positive). We need to return the resultant array. See examples below.

```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        asteroids = [(i, i<0) for i in asteroids]
        result = []
        while asteroids:
            if result and result[-1][1] and not asteroids[-1][1]:
                asteroids.append(result.pop())
            elif len(asteroids) > 1 and asteroids[-1][1] and not asteroids[-2][1]:
                left = asteroids.pop()
                right = asteroids.pop()
                if abs(left[0]) < abs(right[0]):
                    asteroids.append(right)
                elif abs(right[0]) < abs(left[0]):
                    asteroids.append(left)
                else:
                    asteroids.append(left)
                    asteroids.append(right)
            else:
                result.append(asteroids.pop())
        return reversed([i[0] for i in result])
```