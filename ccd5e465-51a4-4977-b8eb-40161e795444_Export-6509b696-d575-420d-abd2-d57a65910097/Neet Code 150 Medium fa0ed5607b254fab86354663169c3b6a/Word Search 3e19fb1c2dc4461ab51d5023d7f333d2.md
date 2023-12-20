# Word Search

Status: Not started
Tags: BackTracking
Last edited time: November 27, 2023 12:36 PM

[https://leetcode.com/problems/word-search/](https://leetcode.com/problems/word-search/)

```python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        rows = len(board)
        cols = len(board[0])
        for i in range(rows):
            for j in range(cols):
                if board[i][j] == word[0]:
                    result = self.check(board, i, j, word, 0)
                    if result:
                        return True
        return False
    
    def check(self, board, i, j, word, wi):
        if wi >= len(word):
            return True
        if board[i][j] != word[wi]:
            return False
        if wi == len(word)-1:
            return True
        contains = False
        for (a,b) in [(-1,0), (0, -1), (1, 0), (0, 1)]:
            ni,nj = a+i, b+j
            if 0 <= ni < len(board) and 0 <= nj < len(board[i]) and board[ni][nj] != '#':
                tmp, board[i][j] = board[i][j], '#'
                contains = contains or self.check(board, ni, nj, word, wi+1)
                board[i][j] = tmp
                if contains:
                    return True
        return contains
```