# Partition Labels

**Link:** https://leetcode.com/problems/partition-labels/

## Approach

First pass: record the last index of every character. Second pass: expand the current partition's `end` to the furthest last index seen so far. When the current position reaches `end`, the partition is complete — record its size and reset.

**Why it works:** A partition must include every occurrence of each character within it. Tracking the furthest last index ensures no character is split across partitions.

## Code

```python
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        lastIndex = {}

        for i, c in enumerate(s):
            lastIndex[c] = i
        
        res = []
        size, end = 0, 0

        for i, c in enumerate(s):
            end = max(end, lastIndex[c])
            size += 1

            if end == i:
                res.append(size)
                size = 0
        
        return res
```

## Complexity

Time: O(n) — two passes over the string  
Space: O(1) — at most 26 entries in `lastIndex`
