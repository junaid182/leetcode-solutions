# Valid Sudoku

**Link:** https://leetcode.com/problems/valid-sudoku/

## Approach

**Brute force:** For each row, column, and 3×3 box, collect all filled values and check for duplicates separately — repetitive and verbose.

**Optimized:** Single pass over the entire board. Track seen values per row, per column, and per 3×3 box using hash sets. The box index is derived as `(r // 3, c // 3)`, giving a unique key for each of the 9 sub-grids. If any value already exists in its row, column, or box set, the board is invalid.

**Why it works:** Each number 1–9 must appear at most once in every row, column, and 3×3 box. Using sets gives O(1) lookup and insertion, and `(r // 3, c // 3)` neatly maps any cell to its box without extra math.

## Code

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = collections.defaultdict(set)
        cols = collections.defaultdict(set)
        squareGrid = collections.defaultdict(set)

        for r in range(9):
            for c in range(9):
                if board[r][c] == ".":
                    continue
                if (board[r][c] in rows[r] or
                    board[r][c] in cols[c] or
                    board[r][c] in squareGrid[r // 3, c // 3]):
                    return False
                rows[r].add(board[r][c])
                cols[c].add(board[r][c])
                squareGrid[r // 3, c // 3].add(board[r][c])

        return True
```

## Complexity

Time: O(1) — board is always 9×9  
Space: O(1) — sets hold at most 81 values total
