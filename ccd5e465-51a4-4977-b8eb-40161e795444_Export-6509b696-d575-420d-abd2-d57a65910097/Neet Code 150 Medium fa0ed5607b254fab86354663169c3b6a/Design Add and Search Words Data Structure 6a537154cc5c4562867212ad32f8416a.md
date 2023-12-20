# Design Add and Search Words Data Structure

Status: Not started
Summary: The "Design Add and Search Words Data Structure" document provides a Python implementation of a WordDictionary class using a Trie data structure. The addWord() method adds a word to the Trie, while the search() method searches for a word in the Trie, allowing wildcard characters. The idea is to recursively traverse the Trie based on the characters in the word, considering wildcard characters as well.
Tags: Trie
Last edited time: November 23, 2023 3:48 PM

```python
class Node:
    def __init__(self, char, isEnd=False):
        self.char = char
        self.isEnd = isEnd
        self.children = {}
    
    def __repr__(self):
        return f"{self.char,self.isEnd,[self.children]}"

class WordDictionary:

    def __init__(self):
        self.trie = Node("#")        

    def addWord(self, word: str) -> None:
        curr = self.trie
        for c in word:
            if c not in curr.children:
                curr.children[c] = Node(c)
            curr = curr.children[c]
        curr.isEnd = True

    def search(self, word: str) -> bool:
        return self.helper(self.trie, word, 0)
    
    def helper(self, lookup, word, index):
        isWord = False
        if index == len(word)-1:
            if word[index] == '.':
                for child in lookup.children:
                    if lookup.children[child].isEnd:
                        isWord = True
                        break
            elif word[index] in lookup.children:
                isWord = lookup.children[word[index]].isEnd
        elif word[index] == '.':
            for c in lookup.children:
                isWord = isWord or self.helper(lookup.children[c], word, index+1)
                if isWord:
                    break
        elif word[index] in lookup.children:
            isWord = self.helper(lookup.children[word[index]], word, index+1)
        return isWord

# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```

Idea:

- Create a Trie
- When you have wildcard character, recurse all children
- If its a character decide to recurse or to break.