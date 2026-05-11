# Max Area of Island

**Link:** https://leetcode.com/problems/max-area-of-island/

## Approach

Same structure as Number of Islands, but DFS returns the size of each island instead of just marking it visited. Each call contributes `1` for the current cell plus the sizes of all four neighbors. Track the maximum across all islands.

## Code

```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        visit = set()

        def dfs(i, j):
            if i >= len(grid) or j >= len(grid[0]) or i < 0 or j < 0 or grid[i][j] == 0:
                return 0
            
            sum = 0

            if (i, j) not in visit:
                visit.add((i, j))
                sum = 1

                sum += dfs(i, j+1)
                sum += dfs(i+1,j)
                sum += dfs(i, j-1)
                sum += dfs(i-1, j)

            return sum

        res = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 1 and (i, j) not in visit:
                    res = max(res, dfs(i, j))
        
        return res
```

## Complexity

Time: O(m × n) — each cell visited at most once  
Space: O(m × n) — visit set and recursion stack
