# Reverse String

**Link:** https://leetcode.com/problems/reverse-string/

## Approach

**Brute force:** Create a new reversed list and copy elements back into `s`. Uses O(n) extra space.

**Optimized:** Use two pointers starting at both ends of the array. Swap the elements at `l` and `r`, then move them inward until they meet. Everything is done in-place.

**Why it works:** Each swap puts both elements in their final reversed position simultaneously. The pointers meet in the middle, so every element is swapped exactly once (or not at all for the middle element in an odd-length array).

## Code

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        l, r = 0, len(s) - 1

        while l < r:
            s[l], s[r] = s[r], s[l]
            l += 1
            r -= 1
```

## Complexity

Time: O(n) — each element is visited at most once
Space: O(1) — in-place, no extra space used
