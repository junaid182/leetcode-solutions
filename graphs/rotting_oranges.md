# Rotting Oranges

**Link:** https://leetcode.com/problems/rotting-oranges/

## Approach

Multi-source BFS starting from all initially rotten oranges simultaneously. Each BFS level represents one minute — rot all reachable fresh neighbors, decrement the fresh count, and increment time. If fresh reaches zero, return the time elapsed; otherwise return `-1`.

**Why it works:** BFS naturally models simultaneous spread — all rotten oranges at minute `t` infect their neighbors at minute `t+1` in the same pass.

## Code

```python
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        q = deque()
        time, fresh = 0, 0

        for r in range(len(grid)):
            for c in range(len(grid[0])):
                if grid[r][c] == 2:
                    q.append([r, c])
                if grid[r][c] == 1:
                    fresh += 1
        
        directions = [[0, 1], [1, 0], [0, -1], [-1, 0]]
        while q and fresh:
            for i in range(len(q)):
                r, c = q.popleft()
                for dr, dc in directions:
                    row, col = dr + r, dc + c

                    if row < 0 or row >= len(grid) or col < 0 or col >= len(grid[0]) or grid[row][col] != 1:
                        continue

                    q.append([row, col])
                    grid[row][col] = 2
                    fresh -= 1
            time += 1
        
        return time if fresh == 0 else -1
```

## Complexity

Time: O(m × n) — each cell processed at most once  
Space: O(m × n) — queue size
