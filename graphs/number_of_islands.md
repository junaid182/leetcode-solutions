# Number of Islands

**Link:** https://leetcode.com/problems/number-of-islands/

## Approach

Scan the grid. When an unvisited land cell (`"1"`) is found, increment the count and DFS to mark all connected land cells as visited. Each DFS call from the outer loop corresponds to one island.

A `visit` set tracks visited cells to avoid revisiting. DFS returns early on out-of-bounds, water, or already-visited cells.

## Code

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        res = 0
        rows, cols = len(grid), len(grid[0])
        visited = set()

        def dfs(r, c):
            if (r, c) in visited:
                return
            
            if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] == "0":
                return
            
            visited.add((r, c))
            dfs(r+1, c)
            dfs(r-1, c)
            dfs(r, c+1)
            dfs(r, c-1)

        for r in range(rows):
            for c in range(cols):
                if (r, c) not in visited and grid[r][c] == "1":
                    dfs(r, c)
                    res += 1
        
        return res
```

## Complexity

Time: O(m × n) — each cell visited at most once  
Space: O(m × n) — visit set and recursion stack
