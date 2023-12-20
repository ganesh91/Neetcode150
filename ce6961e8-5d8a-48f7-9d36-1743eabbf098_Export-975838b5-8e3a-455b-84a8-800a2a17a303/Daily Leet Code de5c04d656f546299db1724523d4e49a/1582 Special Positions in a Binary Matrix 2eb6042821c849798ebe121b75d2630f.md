# 1582. Special Positions in a Binary Matrix

Status: Not started
Tags: Matrix

```jsx
class Solution:
    def numSpecial(self, mat: List[List[int]]) -> int:
        m = len(mat)
        n = len(mat[0])
        m_rows = [0 for i in range(m)]
        n_cols = [0 for i in range(n)]
        
        for row in range(m):
            for col in range(n):
                m_rows[row]+= mat[row][col]
                n_cols[col]+= mat[row][col]
        
        result = 0

        for row in range(m):
            if m_rows[row] > 0:
                for col in range(n):
                    if mat[row][col] == 1 and m_rows[row] == 1 and n_cols[col] == 1:
                        result += 1
        
        return result
```