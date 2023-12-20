# Palindrome Substrings

Status: Not started
Tags: Dynamic Programming, Two Pointers
Last edited time: December 1, 2023 7:33 PM

[https://leetcode.com/problems/palindromic-substrings/](https://leetcode.com/problems/palindromic-substrings/)

Version 1

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        # dp = [[-1 for i in range(len(s))] for j in range(len(s))]
        counts = 0

        for k in range(len(s)):
            i,j = self.bounds(s, k,k)
            while i <= j:
                # dp[j-i][i] += 1
                counts+=1
                i+=1
                j-=1
        
            x,y = self.bounds(s,k,k+1)
            while x < y:
                # dp[y-x][x] +=1
                counts +=1
                x+=1
                y-=1

        # for i in range(len(dp)):
        #     for j in range(len(dp)):
        #         if dp[i][j] >= 0:
        #             counts += 1
        
        # for i in dp:
        #     print(i)
        
        return counts
    

    def bounds(self,s,a,b):
        i,j = a,b
        while i >= 0 and j < len(s) and s[i] == s[j]:
            i-=1
            j+=1
        return i+1, j-1
```

Code 2:

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        dp = [[-1 for i in range(len(s))] for j in range(len(s))]
        counts = 0

        for k in range(len(s)):
            i,j = self.bounds(s, k,k)
            while i <= j:
                dp[j-i][i] += 1
                # counts+=1
                i+=1
                j-=1
        
            x,y = self.bounds(s,k,k+1)
            while x < y:
                dp[y-x][x] +=1
                # counts +=1
                x+=1
                y-=1

        for i in range(len(dp)):
            for j in range(len(dp)):
                if dp[i][j] >= 0:
                    counts += 1
        
        # for i in dp:
        #     print(i)
        
        return counts
    

    def bounds(self,s,a,b):
        i,j = a,b
        while i >= 0 and j < len(s) and s[i] == s[j]:
            i-=1
            j+=1
        return i+1, j-1
```

Code 3:

```python
counts = 0
        even_cache = {}
        odd_cache = {}
        for windowsize in range(0, len(s)):
            for start in range(0, len(s)):
                if start+windowsize < len(s):
                    cache = odd_cache if windowsize % 2 == 0 else even_cache
                    counts += self.is_palindrome_v2(s, start, start+windowsize, cache)
        return counts
    
    def is_palindrome(self, s, left, right):
        while left <= right:
            if s[left] == s[right]:
                left += 1
                right -= 1
            else:
                return 0
        return 1
    
    def is_palindrome_v2(self, s, left, right, cache):
        if left == right:
            return 1
        #[A,A] => 0,1 diff = 1-0 = 1
        #[A,A,A] => 0,2 diff = 2-0 = 2
        diff = right - left
        mid = left + diff//2
        ptr1, ptr2 = (mid-1, mid+1) if diff % 2 == 0 else (mid, mid+1)

        if mid in cache:
            if cache[mid] == -1:
                return 0
            else:
                ptr1 = ptr1-cache[mid]
                ptr2 = ptr2+cache[mid]
        
        result = 1
        while ptr1 >= left and ptr2 <= right:
            if s[ptr1] == s[ptr2]:
                ptr1-=1
                ptr2+=1
            else:
                result = 0
                break
        
        if result == 0:
            cache[mid] = -1
        else:
            cache[mid] = diff//2
        
        return result
```