# Valid SudoKU

Status: Not started
Summary: The provided code is a Python solution to the problem "Valid Sudoku" on LeetCode. The code checks if a given Sudoku board is valid by ensuring that each row, column, and 3x3 sub-grid contains unique numbers from 1 to 9. The code uses lookup dictionaries to keep track of numbers in each row, column, and sub-grid, and returns True if the board is valid and False otherwise.
Tags: Array
Last edited time: November 24, 2023 11:01 AM

[https://leetcode.com/problems/valid-sudoku/](https://leetcode.com/problems/valid-sudoku/)

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        mini_grid_lookup = {}
        x_lookup = {}
        y_lookup = {}

        for i in range(len(board)):
            x_lookup[i] = set([])
            y_lookup[i] = set([])
        
        for i in range(len(board)):
            for j in range(len(board)):
                x,y = i//3, j//3

                if x not in mini_grid_lookup:
                    mini_grid_lookup[x] = {}
                if y not in mini_grid_lookup[x]:
                    mini_grid_lookup[x][y] = set([])

                if board[i][j]!= '.' and board[i][j] in mini_grid_lookup[x][y]:
                    return False
                mini_grid_lookup[x][y].add(board[i][j])

                if board[i][j]!= '.' and board[i][j] in x_lookup[i]:
                    return False
                x_lookup[i].add(board[i][j])

                if board[i][j]!= '.' and board[i][j] in y_lookup[j]:
                    return False
                y_lookup[j].add(board[i][j])
        
        return True
```