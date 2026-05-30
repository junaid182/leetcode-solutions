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

        def backtrack(openP, closedP, path):
            if openP == closedP == n:
                res.append("".join(path))
                return

            if openP < n:
                path.append('(')
                backtrack(openP+1, closedP, path)
                path.pop()
            
            if openP > closedP:
                path.append(')')
                backtrack(openP, closedP+1, path)
                path.pop()

        backtrack(0, 0, [])

        return res
```

## Complexity

Time: O(4^n / √n) — nth Catalan number of valid combinations  
Space: O(n) — recursion depth and stack size
