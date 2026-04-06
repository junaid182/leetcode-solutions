# Car Fleet

**Link:** https://leetcode.com/problems/car-fleet/

## Approach

**Brute force:** Simulate each car's position over time and detect when they merge. Complex and expensive.

**Optimized:** Sort cars by starting position in descending order (closest to target first). Compute each car's time to reach the target. Use a stack to track fleet arrival times — if the current car takes longer than the car ahead (top of stack), it can never catch up and forms a new fleet; push it. If it's faster or equal, it catches up and joins the fleet ahead, so discard it.

**Why it works:** Processing from closest to target outward means a car can only be blocked by cars already on the stack (those ahead of it). If it arrives later, it's slower and will be caught — forming one fleet with the car ahead. The stack size is the number of distinct fleets.

## Code

```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        pairs = [[p, s] for p, s in zip(position, speed)]
        stack = []

        for p, s in sorted(pairs)[::-1]:
            time = (target - p) / s
            if not stack or time > stack[-1]:
                stack.append(time)

        return len(stack)
```

## Complexity

Time: O(n log n) — dominated by sorting
Space: O(n) — stack and pairs list
