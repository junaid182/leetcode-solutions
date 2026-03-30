# Valid Parentheses

**Link:** https://leetcode.com/problems/valid-parentheses/

## Approach

**Brute force:** Repeatedly scan the string and remove matched pairs until no more can be removed, then check if empty. O(n²) time.

**Optimized:** Use a stack. Push opening brackets onto the stack. When a closing bracket is encountered, check if the top of the stack holds its matching opener — if not, return False. At the end, the stack must be empty.

**Why it works:** A stack naturally tracks the most recent unmatched opener. Every closing bracket must match the innermost unmatched opener, which is exactly what the stack top represents.

## Code

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        match = {')': '(', '}': '{', ']': '['}

        for c in s:
            if c in match:
                if not stack or stack.pop() != match[c]:
                    return False
            else:
                stack.append(c)

        return len(stack) == 0
```

## Complexity

Time: O(n)
Space: O(n)
