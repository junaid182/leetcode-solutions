# Merge Intervals

**Link:** https://leetcode.com/problems/merge-intervals/

## Approach

Sort by start time. Seed the result with the first interval. For each subsequent interval, compare its start against the last result's end — if they overlap (`start <= lastEnd`), extend the last interval's end to the max of both ends. Otherwise append as a new interval.

## Code

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda x:x[0])
        res = [intervals[0]]

        for start, end in intervals:
            lastEnd = res[-1][1]

            if start <= lastEnd:
                res[-1][1] = max(lastEnd, end)
            else:
                res.append([start, end])
        
        return res
```

## Complexity

Time: O(n log n) — dominated by sorting  
Space: O(n) — output list
