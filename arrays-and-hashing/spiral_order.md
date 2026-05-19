# Spiral Matrix

**Link:** https://leetcode.com/problems/spiral-matrix/

## Approach

Maintain four boundaries: `left`, `right`, `top`, `bottom`. Each pass of the while loop traces one full spiral layer — right across the top, down the right side, left across the bottom, up the left side. Shrink the boundary after each direction. The mid-loop guard handles non-square matrices where the layer may be exhausted after the right or bottom pass.

## Code

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        left, right = 0, len(matrix[0])
        top, bottom = 0, len(matrix)

        while left < right and top < bottom:
            
            for i in range(left, right):
                res.append(matrix[top][i])
            top += 1

            for i in range(top, bottom):
                res.append(matrix[i][right - 1])
            right -= 1

            if not (left < right and top < bottom):
                break

            for i in range(right-1, left-1, -1):
                res.append(matrix[bottom-1][i])
            bottom -= 1

            for i in range(bottom-1, top-1, -1):
                res.append(matrix[i][left])
            left += 1
        
        return res
```

## Complexity

Time: O(m × n) — every cell visited once  
Space: O(1) — excluding the output array
