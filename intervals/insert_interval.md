# Insert Interval

**Link:** https://leetcode.com/problems/insert-interval/

## Approach

Iterate through existing intervals with three cases:

1. **New interval ends before current starts** (`newInterval[1] < intervals[i][0]`): no more overlaps possible — append `newInterval` and return with the remaining intervals.
2. **New interval starts after current ends** (`newInterval[0] > intervals[i][1]`): no overlap — append current interval and move on.
3. **Overlap**: merge by taking the min start and max end into `newInterval` and continue.

After the loop, append the (possibly merged) `newInterval`.

## Code

```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        res = []

        for i in range(len(intervals)):
            if newInterval[1] < intervals[i][0]:
                res.append(newInterval)
                return res + intervals[i:]
            elif newInterval[0] > intervals[i][1]:
                res.append(intervals[i])
            else:
                newInterval = [min(newInterval[0], intervals[i][0]), max(newInterval[1], intervals[i][1])]
        
        res.append(newInterval)

        return res
```

## Complexity

Time: O(n) — single pass through intervals  
Space: O(n) — output list
