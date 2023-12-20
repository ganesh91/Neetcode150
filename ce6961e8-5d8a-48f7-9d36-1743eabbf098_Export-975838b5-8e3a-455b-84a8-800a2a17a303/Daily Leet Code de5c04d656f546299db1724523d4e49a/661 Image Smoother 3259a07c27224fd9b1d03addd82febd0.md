# 661. Image Smoother

Status: Not started
Tags: Matrix

[https://leetcode.com/problems/image-smoother/](https://leetcode.com/problems/image-smoother/)

```python
class Solution:
    def imageSmoother(self, img: List[List[int]]) -> List[List[int]]:
        result = [[0 for col in range(len(img[0]))] for row in range(len(img))]
        kernel = 3//2

        for row in range(len(img)):
            sum_so_far, elements_so_far = 0, 0
            for col in range(len(img[0])):
                if col == 0:
                    sum_mod, element_mod = self.expand(row, col, kernel, img)
                    sum_so_far += sum_mod
                    elements_so_far += element_mod
                sum_mod, element_mod = self.contract(row,col-1, kernel, img)
                sum_so_far += sum_mod
                elements_so_far += element_mod
                sum_mod, element_mod = self.expand(row,col+1,kernel, img)
                sum_so_far += sum_mod
                elements_so_far += element_mod
                result[row][col] = sum_so_far//elements_so_far
        
        return result
    
    def expand(self, row, col, kernel, img):
        sm, i = 0,0
        if col < len(img[0]):
            for n_row in range(row-kernel, row+kernel+1):
                if 0 <= n_row < len(img):
                    sm += img[n_row][col]
                    i += 1
        return sm, i
    
    def contract(self, row, col, kernel, img):
        sm, i = 0,0
        if col-1 >= 0:
            for n_row in range(row-kernel, row+kernel+1):
                if 0 <= n_row < len(img):
                    sm -= img[n_row][col-1]
                    i -= 1
        return sm, i
```