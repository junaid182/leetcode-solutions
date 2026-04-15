# Min Stack

**Link:** https://leetcode.com/problems/min-stack/

## Approach

**Brute force:** On every `getMin()` call, scan the entire stack to find the minimum. O(n) per `getMin()` call.

**Optimized:** Maintain a parallel `minStack` that tracks the current minimum at every level of the main stack. On each push, append `min(val, minStack[-1])` to `minStack`. On each pop, pop from both stacks simultaneously.

**Why it works:** The `minStack` mirrors the main stack in size, so each index in `minStack` holds the minimum of all elements in the main stack up to that depth. Popping keeps them in sync, so `minStack[-1]` always reflects the current minimum in O(1).

## Code

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.minstack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        minVal = min(val, self.minstack[-1] if self.minstack else val)
        self.minstack.append(minVal)

    def pop(self) -> None:
        self.stack.pop()
        self.minstack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minstack[-1]
```

## Complexity

Time: O(1) — all operations (push, pop, top, getMin) are constant time
Space: O(n) — minStack stores one entry per pushed element
