# Surrounded Regions

**Link:** https://leetcode.com/problems/surrounded-regions/

## Approach

Any `"O"` connected to the border cannot be captured. DFS from every border cell, marking reachable `"O"`s as `"S"` (safe). Then one pass converts remaining `"O"` → `"X"` (captured) and `"S"` → `"O"` (restore safe cells).

**Why it works:** Instead of identifying which `"O"`s are surrounded (hard), identify which ones are *not* surrounded (easy — any connected to the border) and protect them.

## Code

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        rows, cols = len(board), len(board[0])

        visited = set()

        def dfs(r, c):
            if (r, c) in visited:
                return
            if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != "O":
                return
            
            visited.add((r,c))
            board[r][c] = "S"
            dfs(r+1, c)
            dfs(r-1, c)
            dfs(r, c+1)
            dfs(r, c-1)

        for r in range(rows):
            for c in [0, cols-1]:
                dfs(r, c)
        
        for c in range(cols):
            for r in [0, rows-1]:
                dfs(r, c)
        
        for r in range(rows):
            for c in range(cols):
                if board[r][c] == "O":
                    board[r][c] = "X"
                elif board[r][c] == "S":
                    board[r][c] = "O"
```

## Complexity

Time: O(m × n) — each cell visited at most once  
Space: O(m × n) — recursion stack
