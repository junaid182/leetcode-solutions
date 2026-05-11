# Number of Islands

**Link:** https://leetcode.com/problems/number-of-islands/

## Approach

Scan the grid. When an unvisited land cell (`"1"`) is found, increment the count and DFS to mark all connected land cells as visited. Each DFS call from the outer loop corresponds to one island.

A `visit` set tracks visited cells to avoid revisiting. DFS returns early on out-of-bounds, water, or already-visited cells.

## Code

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        visit = set()

        def dfs(i, j):
            if i >= len(grid) or j >= len(grid[0]) or i < 0 or j < 0 or grid[i][j] == "0":
                return

            if (i, j) not in visit:
                visit.add((i, j))

                dfs(i, j+1)
                dfs(i+1,j)
                dfs(i, j-1)
                dfs(i-1, j)

        res = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == "1" and (i, j) not in visit:
                    res += 1
                    dfs(i, j)
        
        return res
```

## Complexity

Time: O(m × n) — each cell visited at most once  
Space: O(m × n) — visit set and recursion stack
