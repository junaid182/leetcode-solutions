# Rotting Oranges

**Link:** https://leetcode.com/problems/rotting-oranges/

## Approach

Multi-source BFS starting from all initially rotten oranges simultaneously. Each BFS level represents one minute — rot all reachable fresh neighbors and increment `minutes`. Return early if there are no fresh oranges. After the loop, return `minutes - 1` (the loop runs one extra iteration after the last batch rots) if all fresh oranges are gone, otherwise `-1`.

**Why it works:** BFS naturally models simultaneous spread — all rotten oranges at minute `t` infect their neighbors at minute `t+1` in the same pass.

## Code

```python
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        queue = deque()
        minutes, fresh = 0, 0

        for r in range(len(grid)):
            for c in range(len(grid[0])):
                if grid[r][c] == 2:
                    queue.append((r, c))
                elif grid[r][c] == 1:
                    fresh += 1
        
        if fresh == 0:
            return 0
        
        directions = [[1,0], [-1, 0], [0, 1], [0, -1]]

        while queue:
            for i in range(len(queue)):
                r, c = queue.popleft()

                for dr, dc in directions:
                    nr, nc = r + dr, c + dc
                    if (0 <= nr < rows) and (0 <= nc < cols) and grid[nr][nc] == 1:
                        grid[nr][nc] = 2
                        fresh -= 1
                        queue.append((nr,nc))
            minutes += 1
        
        return minutes - 1 if fresh == 0 else -1
```

## Complexity

Time: O(m × n) — each cell processed at most once  
Space: O(m × n) — queue size
