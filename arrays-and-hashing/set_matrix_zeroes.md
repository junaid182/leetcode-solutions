# Set Matrix Zeroes

**Link:** https://leetcode.com/problems/set-matrix-zeroes/

## Approach

Use the first row and first column as markers to avoid extra space. First pass: for each zero at `(r, c)`, mark `matrix[0][c] = 0` and `matrix[r][0] = 0`. The first row itself is a special case — track it separately with `rowZero` to avoid conflating it with the column marker.

Second pass: zero out cells `(r, c)` for `r > 0, c > 0` if their row or column marker is zero. Then handle the first column (if `matrix[0][0] == 0`) and first row (if `rowZero`) separately.

## Code

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        rows, cols = len(matrix), len(matrix[0])
        rowZero = False

        for r in range(rows):
            for c in range(cols):
                if matrix[r][c] == 0:
                    matrix[0][c] = 0

                    if r > 0:
                        matrix[r][0] = 0
                    else:
                        rowZero = True
        
        for r in range(1, rows):
            for c in range(1, cols):
                if matrix[0][c] == 0 or matrix[r][0] == 0:
                    matrix[r][c] = 0
        
        if matrix[0][0] == 0:
            for r in range(rows):
                matrix[r][0] = 0
        
        if rowZero:
            for c in range(cols):
                matrix[0][c] = 0
```

## Complexity

Time: O(m × n) — two passes over the matrix  
Space: O(1) — markers stored in-place
