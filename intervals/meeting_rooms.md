# Meeting Rooms

**Link:** https://leetcode.com/problems/meeting-rooms/

## Approach

Sort intervals by start time. Then scan adjacent pairs — if any meeting ends after the next one starts, there's an overlap and attendance is impossible.

**Why it works:** Sorting guarantees that if any two meetings overlap, they will be adjacent in the sorted order. Checking all non-adjacent pairs is unnecessary.

## Code

```python
class Solution:
    def canAttendMeetings(self, intervals: List[Interval]) -> bool:
        intervals.sort(key=lambda x: x.start)

        for i in range(len(intervals) - 1):
            if intervals[i].end > intervals[i+1].start:
                return False
        
        return True
```

## Complexity

Time: O(n log n) — dominated by sorting  
Space: O(1) — no extra space beyond the sort
