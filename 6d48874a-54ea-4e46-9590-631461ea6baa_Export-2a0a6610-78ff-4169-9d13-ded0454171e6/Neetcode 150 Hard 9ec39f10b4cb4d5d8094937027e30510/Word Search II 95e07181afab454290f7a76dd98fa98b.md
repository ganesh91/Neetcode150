# Word Search II

Status: Not started
Tags: Backtracking, Trie
Created time: December 16, 2023 10:21 PM

[https://leetcode.com/problems/word-search-ii/description/](https://leetcode.com/problems/word-search-ii/description/)

```python
from dataclasses import dataclass, field

@dataclass
class Trie:
    char: str
    nodes: dict = field(default_factory=lambda: {})
    isEnd: bool = False

class Solution:
    def __init__(self):
        self.trie = Trie('#')
    
    def addWords(self, word):
        current = self.trie
        for c in word:
            if c not in current.nodes:
                current.nodes[c] = Trie(c)
            current = current.nodes[c]
        current.isEnd = True

    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        for word in words:
            self.addWords(word)
        
        rows = len(board)
        cols = len(board[0])

        collector = []
        for row in range(rows):
            for col in range(cols):
                if board[row][col] in self.trie.nodes:
                    self.traverse(row, col, board, [], collector, self.trie.nodes[board[row][col]])
        return list(set(collector))
        
    
    def traverse(self, row, col, board, path, collector, trie):
        path.append(board[row][col])
        if trie.isEnd:
            collector.append("".join(path))
        tmp, board[row][col] = board[row][col], '#'
        for a,b in [(-1,0), (0, -1), (1,0), (0,1)]:
            x = a+row
            y = b+col
            if 0 <= x < len(board) and 0 <= y < len(board[0]) and board[x][y] in trie.nodes:
                self.traverse(x, y, board, path, collector, trie.nodes[board[x][y]])
        board[row][col] = tmp
        path.pop()
```