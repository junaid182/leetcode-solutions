# Evaluate Reverse Polish Notation

**Link:** https://leetcode.com/problems/evaluate-reverse-polish-notation/

## Approach

**Brute force:** Repeatedly scan the token list for an operator preceded by two numbers, evaluate it, replace the three tokens with the result, and repeat until one token remains. O(n²) time.

**Optimized:** Use a stack. Push numbers as they appear. When an operator is encountered, pop the top two values, apply the operation, and push the result back. The final value on the stack is the answer.

**Why it works:** RPN is defined such that an operator always follows its two operands. A stack naturally preserves ordering — the last pushed number is the most recent operand, so popping two gives the correct pair. Division truncates toward zero, handled with `int(b / a)` instead of `b // a` (which floors, not truncates).

## Code

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        operators = ['+', '-', '*', '/']

        for t in tokens:
            if t in operators:
                a = stack.pop()
                b = stack.pop()

                if t == '+':
                    stack.append(b + a)
                elif t == '-':
                    stack.append(b - a)
                elif t == '*':
                    stack.append(b * a)
                else:
                    stack.append(int(b / a))

            else:
                stack.append(int(t))

        return stack[0]
```

## Complexity

Time: O(n) — single pass through the token list
Space: O(n) — stack holds at most n/2 numbers at a time
