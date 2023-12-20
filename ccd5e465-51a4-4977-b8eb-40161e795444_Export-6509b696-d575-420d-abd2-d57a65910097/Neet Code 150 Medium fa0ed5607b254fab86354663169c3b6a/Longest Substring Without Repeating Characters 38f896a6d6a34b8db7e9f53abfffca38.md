# Longest Substring Without Repeating Characters

Status: Not started
Tags: Sliding Window, String, Two Pointers
Last edited time: November 28, 2023 8:15 PM

[https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        max_len = 0
        start = 0
        current = 0
        seen = set([])
        while current < len(s):
            if s[current] not in seen:
                seen.add(s[current])
                current += 1
            else:
                seen.remove(s[start])
                start += 1

            max_len = max(max_len, current-start)
        return max_len
```