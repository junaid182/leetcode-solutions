# Baseball Game

**Link:** https://leetcode.com/problems/baseball-game/

## Approach

**Brute force:** Simulate all operations using a list, processing each string one at a time.

**Optimized:** Use a stack to track scores. For each operation: `C` pops the last score, `D` pushes double the last score, `+` pushes the sum of the last two scores, and any integer string gets pushed directly.

**Why it works:** A stack naturally models the "last recorded score" access pattern. Each operation only needs to look at the top 1 or 2 elements, making this O(1) per operation.

## Code

```python
class Solution:
    def calPoints(self, operations: List[str]) -> int:
        stack = []

        for oper in operations:
            if oper == 'C':
                stack.pop()
            elif oper == 'D':
                stack.append(int(stack[-1]) * 2)
            elif oper == '+':
                stack.append(int(stack[-1]) + int(stack[-2]))
            else:
                stack.append(int(oper))

        return sum(stack)
```

## Complexity

Time: O(n)
Space: O(n)
