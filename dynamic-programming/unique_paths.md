# Unique Paths

**Link:** https://leetcode.com/problems/unique-paths/

## Approach

**Brute force:** Recursive DFS from top-left to bottom-right, branching right and down at each step. Exponential time without memoization.

**Optimized:** DP with space optimization. The number of paths to any cell equals paths from the cell above plus paths from the cell to the left. Initialize a `row` of all 1s (bottom row). For each row above, compute a new row right-to-left: `newRow[c] = newRow[c+1] + row[c]`. Replace `row` after each iteration. `row[0]` is the answer.

**Why it works:** The bottom row and rightmost column always have exactly one path (go straight). Every other cell accumulates from its right and bottom neighbors. Scanning right-to-left lets us use `newRow[c+1]` (already updated) as the "from right" contribution.

## Code

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        row = [1] * n

        for r in range(m-1):
            newRow = [1] * n

            for c in range(n-2, -1, -1):
                newRow[c] = newRow[c+1] + row[c]
            row = newRow
        
        return row[0]
```

## Complexity

Time: O(m × n) — fills every cell once  
Space: O(n) — two rows at a time
