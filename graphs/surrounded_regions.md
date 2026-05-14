# Surrounded Regions

**Link:** https://leetcode.com/problems/surrounded-regions/

## Approach

Any `"O"` connected to the border cannot be captured. DFS from every border `"O"`, temporarily marking those cells `"T"`. Then make two passes: flip remaining `"O"` to `"X"` (captured), and restore `"T"` back to `"O"` (safe).

**Why it works:** Instead of identifying which `"O"`s are surrounded (hard), identify which ones are *not* surrounded (easy — any connected to the border) and protect them.

## Code

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        rows, cols = len(board), len(board[0])

        def capture(r, c):
            if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != "O":
                return
            board[r][c] = "T"
            capture(r, c+1)
            capture(r+1, c)
            capture(r, c-1)
            capture(r-1, c)
        
        for r in range(rows):
            for c in range(cols):
                if board[r][c] == "O" and (r == rows-1 or r == 0 or c == cols-1 or c == 0):
                    capture(r, c)
    
        for r in range(rows):
            for c in range(cols):
                if board[r][c] == "O":
                    board[r][c] = "X"

        for r in range(rows):
            for c in range(cols):
                if board[r][c] == "T":
                    board[r][c] = "O"
```

## Complexity

Time: O(m × n) — each cell visited at most once  
Space: O(m × n) — recursion stack
