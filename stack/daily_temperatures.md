# Daily Temperatures

**Link:** https://leetcode.com/problems/daily-temperatures/

## Approach

**Brute force:** For each day, scan forward until a warmer temperature is found. O(n²) time.

**Optimized:** Use a monotonic decreasing stack storing indices. For each day, pop all stack entries whose temperature is lower than the current — those days have now found their next warmer day. Push the current index onto the stack. Any entries remaining after the full pass never find a warmer day (result stays 0).

**Why it works:** The stack maintains indices of temperatures in decreasing order. When a warmer temperature arrives, it resolves all pending cooler days at once. The index difference gives the number of days waited.

## Code

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        res = [0] * len(temperatures)
        stack = []  # indices

        for index, temp in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < temp:
                prev_index = stack[-1]
                res[prev_index] = index - prev_index
                stack.pop()
            stack.append(index)

        return res
```

## Complexity

Time: O(n) — each index is pushed and popped at most once
Space: O(n) — stack holds at most n entries
