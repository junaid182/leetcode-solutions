# Longest Consecutive Sequence

**Link:** https://leetcode.com/problems/longest-consecutive-sequence/

## Approach

**Brute force:** Sort the array and scan for consecutive runs — O(n log n).

**Optimized:** Convert to a set for O(1) lookups. Only start counting a sequence from a number `n` where `n - 1` is not in the set — meaning `n` is the start of a sequence. Then extend the sequence forward while consecutive values exist.

**Why it works:** Skipping non-starts ensures each sequence is counted exactly once, giving O(n) overall despite the nested while loop.

## Code

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        numsSet = set(nums)
        longest = 0

        for n in numsSet:
            if n - 1 not in numsSet:
                length = 0
                while n + length in numsSet:
                    length += 1
                longest = max(longest, length)

        return longest
```

## Complexity

Time: O(n)  
Space: O(n)
