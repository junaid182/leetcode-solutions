# Valid Parentheses

**Link:** https://leetcode.com/problems/valid-parentheses/

## Approach

**Brute force:** Repeatedly scan the string and remove matched adjacent pairs until no more can be removed, then check if the string is empty. O(n²) time.

**Optimized:** Use a stack. Push opening brackets onto the stack. When a closing bracket is encountered, check if the top of the stack holds its matching opener — if yes, pop it; if no, the string is invalid.

**Why it works:** A stack naturally tracks the most recently opened bracket. Every closing bracket must match the innermost unmatched opener, which is always at the top of the stack. If the stack is empty at the end, all brackets were matched.

## Code

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        paranMap = {')': '(', '}': '{', ']': '['}

        for c in s:
            if c in paranMap:
                if stack and stack[-1] == paranMap[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)

        return not stack
```

## Complexity

Time: O(n) — single pass through the string
Space: O(n) — stack holds at most n/2 opening brackets
