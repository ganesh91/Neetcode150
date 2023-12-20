# Encode and Decode Strings

Status: Not started
Tags: String
Last edited time: November 25, 2023 12:48 PM

[https://leetcode.com/problems/encode-and-decode-strings/editorial/](https://leetcode.com/problems/encode-and-decode-strings/editorial/)

Idea:

- Use `//` as escape character

```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        result = []
        for i in strs:
            for c in i:
                if c == '/':
                    result.append("//")
                else:
                    result.append(c)
            result.append("/:")
        return "".join(result)

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        # Edge case: //// => [""]
        current = 0
        result = []
        current_arr = []
        while current < len(s):
            if s[current] == '/' and s[current+1] == '/':
                current_arr.append("/")
                current +=2
            elif s[current] == '/' and s[current+1] == ':':
                result.append("".join(current_arr))
                current += 2
                current_arr = []
            else:
                current_arr.append(s[current])
                current += 1
        return result

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```