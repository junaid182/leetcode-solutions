# Meeting Rooms II

**Link:** https://leetcode.com/problems/meeting-rooms-ii/

## Approach

Sort starts and ends independently. Use two pointers to simulate a sweep line: if the next meeting starts before the earliest ending one, a new room is needed (`count += 1`, advance `sI`). Otherwise a room frees up (`count -= 1`, advance `eI`). Track the peak `count`.

**Why it works:** Sorting ends separately lets us greedily match each new start against the earliest available room end, without needing to track which specific room ends when.

## Code

```python
class Solution:
    def minMeetingRooms(self, intervals: List[Interval]) -> int:
        start = sorted(i.start for i in intervals)
        end = sorted(i.end for i in intervals)
        
        res, count = 0, 0
        sI, eI = 0, 0

        while sI < len(start):
            if start[sI] < end[eI]:
                sI += 1
                count += 1
            else:
                eI += 1
                count -= 1
            res = max(res, count)
        
        return res
```

## Complexity

Time: O(n log n) — sorting both arrays  
Space: O(n) — two sorted arrays
