# Set Matrix Zeroes

Status: Not started
Tags: Math, Matrix
Last edited time: November 27, 2023 8:33 PM

[https://leetcode.com/problems/set-matrix-zeroes/description/](https://leetcode.com/problems/set-matrix-zeroes/description/)

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        row_clear = False
        column_clear = False
        
        for i in matrix[0]:
            if i == 0:
                row_clear = True
                break
        
        for i in range(len(matrix)):
            if matrix[i][0] == 0:
                column_clear = True
                break

        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0
                    matrix[0][j] = 0
        
        for i in range(1, len(matrix)):
            for j in range(1, len(matrix[0])):
                if matrix[0][j] == 0 or matrix[i][0] == 0:
                    matrix[i][j] = 0
        
        if row_clear:
            for i in range(len(matrix[0])):
                matrix[0][i] = 0
        
        if column_clear:
            for i in range(len(matrix)):
                matrix[i][0] = 0
```