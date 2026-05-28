# Generate Parentheses

**Link:** https://leetcode.com/problems/generate-parentheses/

## Approach

Backtracking with two counters: `openN` and `closedN`. Two rules enforce validity at every step:
- Add `(` only if `openN < n`
- Add `)` only if `closedN < openN`

When both equal `n`, the combination is complete. This generates only valid strings without needing to validate after the fact.

## Code

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []

        def backtrack(path, open_count, closed_count):
            if open_count == closed_count == n:
                res.append("".join(path))
            
            if open_count < n:
                path.append("(")
                backtrack(path, open_count+1, closed_count)
                path.pop()
            
            if closed_count < open_count:
                path.append(")")
                backtrack(path, open_count, closed_count+1)
                path.pop()

        backtrack([], 0, 0)

        return res
```

## Complexity

Time: O(4^n / √n) — nth Catalan number of valid combinations  
Space: O(n) — recursion depth and stack size
