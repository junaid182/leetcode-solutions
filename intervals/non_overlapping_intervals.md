# Non-overlapping Intervals

**Link:** https://leetcode.com/problems/non-overlapping-intervals/

## Approach

Sort by start time. Track `prevEnd` — the end of the last kept interval. For each interval:
- **No overlap** (`start >= prevEnd`): keep it, update `prevEnd`.
- **Overlap**: remove one interval (`res += 1`) and greedily keep the one with the smaller end (`prevEnd = min(end, prevEnd)`) — a shorter interval leaves more room for future ones.

## Code

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key=lambda x:x[0])
        res = 0
        prevEnd = intervals[0][1]

        for start, end in intervals[1:]:
            if start >= prevEnd:
                prevEnd = end
            else:
                res += 1
                prevEnd = min(end, prevEnd)
                
        return res
```

## Complexity

Time: O(n log n) — dominated by sorting  
Space: O(1)
