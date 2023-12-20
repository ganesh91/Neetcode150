# Evaluate Reverse Polish Notation

Status: Not started
Summary: The document provides a Python solution to evaluate Reverse Polish Notation (RPN). It uses a stack to perform the evaluation and includes a division function to handle negative numbers correctly. The solution is based on a problem from LeetCode.
Tags: Stack
Last edited time: November 23, 2023 4:30 PM

```python
class Solution:
    def div(self, x, y):
        sign = (-1 if x < 0 else 1) * (-1 if y < 0 else 1)
        return sign * (abs(x)//abs(y))
        
    def evalRPN(self, tokens: List[str]) -> int:
        ops = {'+': lambda x,y: int(x)+int(y),
        '-': lambda x,y: int(x)-int(y),
        '*': lambda x,y: int(x)*int(y),
        '/': lambda x,y: self.div(int(x),int(y))
        }

        stack = []
        for i in tokens:
            if i in ops:
                s = stack.pop()
                f = stack.pop()
                stack.append(ops[i](f,s))
                print(f"Resolving {f}{i}{s}={stack[-1]}")
            else:
                stack.append(i)
        
        return int(stack[-1])
```

Idea:

- Use stack to evaluate
- [https://leetcode.com/problems/evaluate-reverse-polish-notation/description/](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)