# Implement Trie

Status: Not started
Tags: Trie
Last edited time: November 25, 2023 6:19 PM

[https://leetcode.com/problems/implement-trie-prefix-tree/](https://leetcode.com/problems/implement-trie-prefix-tree/)

```python
from dataclasses import dataclass, field

@dataclass
class TrieNode:
    char: str
    isEnd: bool = False
    children:dict = field(default_factory=dict)

class Trie:

    def __init__(self):
        self.root = TrieNode('#')

    def insert(self, word: str) -> None:
        current = self.root
        for c in word:
            if c not in current.children:
                current.children[c] = TrieNode(c)
            current = current.children[c]
        current.isEnd = True
        

    def search(self, word: str) -> bool:
        current = self.root
        for c in word:
            if c not in current.children:
                return False
            else:
                current = current.children[c]
        return current.isEnd
        

    def startsWith(self, prefix: str) -> bool:
        current = self.root
        for c in prefix:
            if c not in current.children:
                return False
            else:
                current = current.children[c]
        return not current == None
        

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```