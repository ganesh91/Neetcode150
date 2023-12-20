# Spiral Matrix

Status: Not started
Tags: Matrix
Last edited time: November 27, 2023 4:48 PM

[https://leetcode.com/problems/spiral-matrix/submissions/](https://leetcode.com/problems/spiral-matrix/submissions/)

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        left, top = 0,0
        right, bottom = len(matrix[0])-1, len(matrix)-1
        result = []

        while top <= bottom and left <= right:
            
            for i in range(left, right+1):
                result.append(matrix[top][i])
            top += 1
            
            for i in range(top, bottom+1):
                result.append(matrix[i][right])
            right -=1
            
            if top-1!= bottom:
                for i in range(right, left-1,-1):
                    result.append(matrix[bottom][i])
                bottom -= 1
                
            if left != right+1:
                for i in range(bottom, top-1, -1):
                    result.append(matrix[i][left])
                left += 1
        
        return result
```