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
        minutes, fresh = 0, 0
        queue = deque()

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 1:
                    fresh += 1
                elif grid[r][c] == 2:
                    queue.append((r, c))
        
        if fresh == 0:
            return 0
        
        visited = set()
        while queue:
            for i in range(len(queue)):
                r, c = queue.popleft()
                visited.add((r, c))

                directions = [[1, 0], [-1, 0], [0, 1], [0, -1]]

                for dr, dc in directions:
                    nr = r + dr
                    nc = c + dc

                    if nr < 0 or nr >= rows or nc < 0 or nc >= cols or grid[nr][nc] != 1 or (nr, nc) in visited:
                        continue

                    if grid[nr][nc] == 1:
                        grid[nr][nc] = 2
                        queue.append((nr, nc))
                        fresh -= 1

            minutes += 1
        
        return minutes - 1 if fresh == 0 else -1
```

## Complexity

Time: O(m × n) — each cell processed at most once  
Space: O(m × n) — queue size
