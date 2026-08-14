# Word Search

**Link:** https://leetcode.com/problems/word-search/

## Approach

Try starting DFS from every cell. At each step, check that the current cell matches `word[i]` and hasn't been used in the current path. Add the cell to `path` before recursing and remove it after — this is the backtrack step that allows other branches to reuse the cell.

Return `True` as soon as the full word is matched (`i == len(word)`).

## Code

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        rows, cols = len(board), len(board[0])

        visited = set()
        def backtrack(r, c, i):
            if len(word) == i:
                return True
            
            if (r, c) in visited:
                return False
            
            if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != word[i]:
                return False
            
            visited.add((r,c))
            res = ( backtrack(r+1, c, i+1) or
                    backtrack(r-1, c, i+1) or
                    backtrack(r, c+1, i+1) or
                    backtrack(r, c-1, i+1)
                )
            visited.remove((r,c))
            
            return res

        for r in range(rows):
            for c in range(cols):
                if backtrack(r, c, 0):
                    return True
        
        return False
```

## Complexity

Time: O(m × n × 4^w) — w is word length; 4 directions explored at each step  
Space: O(w) — path set and recursion stack bounded by word length
