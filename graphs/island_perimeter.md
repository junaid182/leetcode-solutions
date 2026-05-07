# Island Perimeter

**Link:** https://leetcode.com/problems/island-perimeter/

## Approach

Start DFS from the first land cell found. Each recursive call contributes `1` to the perimeter when it hits a boundary (out-of-bounds or water) — those are exposed edges. Mark visited cells as `-1` to avoid revisiting.

**Why it works:** Every land cell has 4 edges. An edge contributes to the perimeter only when the neighbor is water or out-of-bounds. DFS naturally counts these by returning `1` at boundaries and `0` at already-visited cells.

## Code

```python
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:

        def dfs(i, j):
            if i < 0 or j < 0 or i >= len(grid) or j >= len(grid[0]) or grid[i][j] == 0:
                return 1
            
            if grid[i][j] == -1:
                return 0

            grid[i][j] = -1
            peri = dfs(i, j+1)
            peri += dfs(i+1, j)
            peri += dfs(i, j-1)
            peri += dfs(i-1, j)

            return peri

        for i in range(len(grid)):
            for j in range(len(grid[i])):
                if grid[i][j] == 1:
                    return dfs(i, j)
```

## Complexity

Time: O(m × n) — each cell visited at most once  
Space: O(m × n) — recursion stack in worst case
