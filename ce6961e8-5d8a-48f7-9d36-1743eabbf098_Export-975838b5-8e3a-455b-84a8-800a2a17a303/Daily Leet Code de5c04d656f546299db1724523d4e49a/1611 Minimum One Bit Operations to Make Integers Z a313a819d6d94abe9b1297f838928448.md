# 1611. Minimum One Bit Operations to Make Integers Zero

Status: Not started
Tags: Math, Recursion

```python
class Solution:
    def minimumOneBitOperations(self, n: int) -> int:
        binary = self.to_bin(n)
        return self.to_zero(binary, 0)
    
    def to_zero(self, binary, n):
        if n >= len(binary):
            return 0
        if n == len(binary)-1:
            if binary[n] == 0:
                return 0
            else:
                binary[n] = 1
                return 1
        if binary[n] == 0:
            return self.to_zero(binary, n+1)
        else:
            x = self.to_one(binary, n+1)
            y = self.to_zero(binary, n+2)
            binary[n] = 0
            return x+y+1 + self.to_zero(binary, n+1)
    
    def to_one(self, binary, n):
        if n >= len(binary):
            return 0
        if n == len(binary)-1:
            if binary[n] == 0:
                binary[n] = 1
                return 1
            else:
                return 0
        if binary[n] == 1:
            return self.to_zero(binary, n+1) 
        else:
            x = self.to_one(binary, n+1)
            y = self.to_zero(binary, n+2)
            binary[n] = 1
            return x+y+1+self.to_zero(binary, n+1)
        

    
    def to_bin(self, n):
        array = []
        while n:
            carry = n % 2
            n = n // 2
            array.append(carry)
        array.reverse()
        return array
```

Idea:

- Convert binary to decimal
- In pure comp-sci way
    - two fns to_zero and to_one needs to happen
    - to_zero will make sure i =0 and to_one make sure i == 1 and returns cost.