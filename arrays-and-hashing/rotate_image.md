# Rotate Image

**Link:** https://leetcode.com/problems/rotate-image/

## Approach

Rotate layer by layer from the outside in, using two pointers `l` and `r`. Within each layer, rotate groups of four cells simultaneously using `i` as an offset (0 to `r-l-1`). A temp variable saves the top-left cell, then the four positions are updated in one cycle:

```
top-left ← bottom-left ← bottom-right ← top-right ← top-left
```

## Code

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        l, r = 0, len(matrix) - 1

        while l < r:
            for i in range(r-l):
                top, bottom = l, r

                topLeft = matrix[top][l+i]

                matrix[top][l+i] = matrix[bottom-i][l]
                matrix[bottom-i][l] = matrix[bottom][r-i]
                matrix[bottom][r-i] = matrix[top+i][r]
                matrix[top+i][r] = topLeft

            l += 1
            r -= 1
```

## Complexity

Time: O(n²) — every cell is visited once  
Space: O(1) — rotated in-place
