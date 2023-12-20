# 1930. Unique Length-3 Palindromic Subsequences

Status: Not started
Tags: Hash Map, Prefix Sum

```python
from collections import defaultdict
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        last_index = defaultdict(int)
        for en, i in enumerate(s):
            last_index[i] = en
        
        count = 0
        
        seen = set([])
        for en,i in enumerate(s):
            if i not in seen and last_index[i] != en:
                seen.add(i)
                chars = set(s[en+1:last_index[i]])
                for j in chars:
                    print(f"{i}{j}{i}")
                count += len(chars)
        
        return count
```