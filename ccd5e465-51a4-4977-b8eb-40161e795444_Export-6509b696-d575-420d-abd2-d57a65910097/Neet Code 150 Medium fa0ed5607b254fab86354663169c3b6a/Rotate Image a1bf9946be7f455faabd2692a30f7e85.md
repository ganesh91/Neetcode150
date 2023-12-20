# Rotate Image

Status: Not started
Tags: Matrix
Last edited time: November 28, 2023 12:32 PM

[https://leetcode.com/problems/rotate-image/](https://leetcode.com/problems/rotate-image/)

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        sq = 0

        N = len(matrix)

        while (N-sq)-sq > 0:
            for i in range(sq, N-sq-1):
                # row is constant
                tmp = matrix[sq][i]

                # col is constant
                print(f"({i},{N-sq-1}) = ({sq},{i})")
                matrix[i][N-sq-1], tmp = tmp, matrix[i][N-sq-1]

                print(f"({N-sq-1},{N-i-1}) = ({i},{N-sq-1})")
                # row is constant
                matrix[N-sq-1][N-i-1], tmp = tmp, matrix[N-sq-1][N-i-1]

                print(f"({N-i-1},{N-sq-1}) = ({N-sq-1},{N-i-1})")
                # column in constant
                matrix[N-i-1][sq], tmp = tmp, matrix[N-i-1][sq]

                print(f"({sq},{i}) = ({N-i-1},{N-sq-1})")
                matrix[sq][i] = tmp
            sq += 1
```