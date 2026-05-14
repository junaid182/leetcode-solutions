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
        
        stack = []
        res = []

        def backtrack(openN, closedN):
            if openN == closedN == n:
                res.append("".join(stack))
                return
            
            if openN < n:
                stack.append("(")
                backtrack(openN + 1, closedN)
                stack.pop()
            
            if closedN < openN:
                stack.append(")")
                backtrack(openN, closedN + 1)
                stack.pop()
        
        backtrack(0, 0)

        return res
```

## Complexity

Time: O(4^n / √n) — nth Catalan number of valid combinations  
Space: O(n) — recursion depth and stack size
