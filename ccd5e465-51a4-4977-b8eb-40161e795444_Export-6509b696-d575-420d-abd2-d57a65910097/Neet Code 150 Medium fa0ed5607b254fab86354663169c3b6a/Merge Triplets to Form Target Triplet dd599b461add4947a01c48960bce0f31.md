# Merge Triplets to Form Target Triplet

Status: Not started
Summary: The "Merge Triplets to Form Target Triplet" problem is solved using a Python solution. The idea is to iterate through the triplets, remove rows that do not have values greater than the corresponding target values, and find the maximum values for each element. If the maximum values match the target triplet, return True; otherwise, return False.
Tags: Greedy
Last edited time: November 24, 2023 11:00 AM

[https://leetcode.com/problems/merge-triplets-to-form-target-triplet/submissions/](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/submissions/)

Idea:

- Inorder to get target triplet, the max value and index can have = target[index]
- Once we remove all rows that do not have it and find argmax, thats the same as doing n! combinations.
- We go argmax across axis and return the result

```python
class Solution:
    def mergeTriplets(self, triplets: List[List[int]], target: List[int]) -> bool:
        acceptable = []
        a,b,c = 0,0,0
        for row in triplets:
            if row[0] > target[0] or row[1] > target[1] or row[2] > target[2]:
                continue
            a,b,c = max(a, row[0]),max(b,row[1]),max(c,row[2])
            if a == target[0] and b == target[1] and c == target[2]:
                return True
        return False
```