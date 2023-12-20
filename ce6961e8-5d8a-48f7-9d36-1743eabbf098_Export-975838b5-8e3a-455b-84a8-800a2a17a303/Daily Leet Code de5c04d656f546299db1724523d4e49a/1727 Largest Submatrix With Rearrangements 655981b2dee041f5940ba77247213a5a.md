# 1727. Largest Submatrix With Rearrangements

Status: Not started
Tags: Prefix Sum

Idea:

- For every row, keep a running sum of continuous column width
- then for every row, sort the columns descending. and calculate area.

```python
class Solution:
    def largestSubmatrix(self, matrix: List[List[int]]) -> int:
        for row in range (1,len(matrix)):
            for column in range(len(matrix[0])):
                if matrix[row][column] != 0:
                    matrix[row][column] += matrix[row-1][column]
        
        max_submatrix = float('-inf')
        for row in matrix:
            row.sort(reverse=True)
            for i in range(len(row)):
                if row[i] == 0:
                    break
                max_submatrix = max(max_submatrix, row[i]*(i+1))
        return max_submatrix if max_submatrix > float('-inf') else 0
```