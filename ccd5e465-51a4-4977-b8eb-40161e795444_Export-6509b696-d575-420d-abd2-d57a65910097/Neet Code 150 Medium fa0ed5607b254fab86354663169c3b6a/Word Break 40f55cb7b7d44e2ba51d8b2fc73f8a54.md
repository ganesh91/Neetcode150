# Word Break

Status: Not started
Tags: Dynamic Programming, Memoization
Last edited time: December 1, 2023 10:53 AM

[https://leetcode.com/problems/word-break/](https://leetcode.com/problems/word-break/)

Version 1: Recursion and Memization

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        lookup = set(wordDict)
        cache = {}
        if s in lookup:
            return True
        return self.breakw(s, 0, lookup, cache)
    

    def breakw(self, word, index, lookup, cache):
        if index >= len(word):
            return True
        if index in cache:
            return cache[index]
        canbreak = False
        for i in range(index, len(word)):
            if word[index:i+1] in lookup:
                canbreak = canbreak or self.breakw(word, i+1, lookup, cache)
        cache[index] = canbreak
        return canbreak
```

Version 2 Using Trie, recursion memoization

```python
class Trie:
    def __init__(self, c, isEnd):
        self.c = c
        self.isEnd = isEnd
        self.children = {}

class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        root = Trie("", False)
        for word in wordDict:
            self.build(root, word)
        return self.wordbreak_helper(s, 0, root, {})

        
    def does_contain(self, s, start, end, root):
        curr = root
        while start <= end:
            c = s[start]
            if c not in curr.children:
                return False
            else:
                curr = curr.children[c]
                start+=1
        return curr.isEnd

    def wordbreak_helper(self, s, idx, root, cache):
        if idx >= len(s):
            return True
        if idx in cache:
            return cache[idx]
        can_split = False
        for j in range(idx, len(s)):
            hasMatch = self.does_contain(s, idx, j, root)
            if hasMatch:
                hasMatch = hasMatch and self.wordbreak_helper(s, j+1, root, cache)
            can_split = can_split or hasMatch
            if can_split:
                break
        cache[idx] = can_split
        return can_split
    
    def build(self, root, s):
        idx = 0
        curr = root
        while idx < len(s):
            isEnd = idx == len(s)-1
            c = s[idx]
            if c in curr.children:
                curr = curr.children[c]
                if isEnd:
                    curr.isEnd = isEnd
            else:
                curr.children[c] = Trie(c, isEnd)
                curr = curr.children[c]
            idx += 1
    
    def printwords(self, trie):
        for child in trie.children:
            self.printhelper(trie.children[child], [])
    
    def printhelper(self, node, collector):
        collector.append(node.c)
        if node.isEnd:
            print("".join(collector))
        for child in node.children:
            self.printhelper(node.children[child], collector)
        collector.pop()
```