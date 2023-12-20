# Surrounded Regions

Status: Not started
Tags: DFS
Last edited time: November 29, 2023 5:22 PM

[https://leetcode.com/problems/surrounded-regions/](https://leetcode.com/problems/surrounded-regions/)

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        global_visited = set([])
        for i in range(len(board)):
            for j in range(len(board[0])):
                if (i,j) not in global_visited and board[i][j] == 'O':
                    visited = set([])
                    captureable = self.recurse(board, i, j, visited)
                    global_visited.update(visited)

                    if captureable:
                        for a,b in visited:
                            board[a][b] = 'X'
    
    def recurse(self, board, i, j, visited):
        if i < 0 or j < 0 or i >= len(board) or j >= len(board[0]):
            return False
        if board[i][j] == 'X':
            return True
        visited.add((i,j))
        captureable = True
        for (a,b) in [(1,0), (0,1), (-1,0), (0, -1)]:
            x,y = a+i, b+j
            if (x,y) not in visited:
                captureable = captureable and self.recurse(board, x, y, visited)
        return captureable
```