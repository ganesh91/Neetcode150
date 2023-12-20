# Min Stack

Status: Not started
Tags: Stack
Last edited time: November 29, 2023 2:17 PM

[https://leetcode.com/problems/min-stack/](https://leetcode.com/problems/min-stack/)

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.mintracker = []
        

    def push(self, val: int) -> None:
        if len(self.stack) == 0:
            self.stack.append(val)
            self.mintracker.append(val)
        else:
            self.stack.append(val)
            if val <= self.mintracker[-1]:
                self.mintracker.append(val)

    def pop(self) -> None:
        item = self.stack.pop()
        if item <= self.mintracker[-1]:
            self.mintracker.pop()
        

    def top(self) -> int:
        return self.stack[-1]
        

    def getMin(self) -> int:
        return self.mintracker[-1]
        

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```