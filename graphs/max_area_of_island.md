# Max Area of Island

**Link:** https://leetcode.com/problems/max-area-of-island/

## Approach

Same structure as Number of Islands, but DFS returns the size of each island instead of just marking it visited. Each call contributes `1` for the current cell plus the sizes of all four neighbors. Track the maximum across all islands.

## Code

```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        res = 0

        visited = set()
        def dfs(r, c):
            if (r, c) in visited:
                return 0
            
            if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] == 0:
                return 0
            
            visited.add((r, c))
            res = 1
            res += dfs(r+1, c)
            res += dfs(r-1, c)
            res += dfs(r, c+1)
            res += dfs(r, c-1)

            return res

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 1:
                    res = max(res, dfs(r, c))
        
        return res
```

## Complexity

Time: O(m × n) — each cell visited at most once  
Space: O(m × n) — visit set and recursion stack
