# 935. Knight Dialer

Status: Not started
Tags: Dynamic Programming

[https://leetcode.com/problems/knight-dialer/](https://leetcode.com/problems/knight-dialer/)

```python
class Solution:
    def __init__(self):
        self.board = [[1,2,3],[4,5,6],[7,8,9],[-1,0,-1]]

    def knightDialer(self, n: int) -> int:
        total = 0
        for row in range(len(self.board)):
            for col in range(len(self.board[0])):
                if self.board[row][col] >= 0:
                    total += self.jump(row, col, n-1)
        return total % (10**9 + 7)

    @cache
    def jump(self, x, y, jumps):
        if jumps <= 0:
            return 1
        combinations = 0
        for nx, ny in self.getNextLocations(x,y):
            combinations += self.jump(nx,ny,jumps-1)
        return combinations % (10**9 + 7)
        
    @cache
    def getNextLocations(self, x,y):
        possible_jumps = [(2,-1),(1,-2),(-1,-2),(-2,-1),(-2,1),(-1,2),(1,2),(2,1)]
        result = []
        for i,j in possible_jumps:
            a = x+i
            b = y+j
            if 0 <= a < len(self.board) and 0 <= b < len(self.board[0]) and self.board[a][b] >= 0:
                result.append([a,b])
        return result
```