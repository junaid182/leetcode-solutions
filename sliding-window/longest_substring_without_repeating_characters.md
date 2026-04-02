# Longest Substring Without Repeating Characters

**Link:** https://leetcode.com/problems/longest-substring-without-repeating-characters/

## Approach
**Brute force:** Check every substring and verify it has no duplicates. O(n²) or O(n³) time.

**Optimized:** Sliding window with a set. Expand the window by moving `j` forward. If `s[j]` is already in the set, shrink the window from the left by removing `s[i]` and advancing `i` until the duplicate is gone. Then add `s[j]` and update the result.

**Why it works:** The set tracks all characters in the current window. Shrinking from the left is safe because any substring starting before `i` that included the duplicate would be shorter than or equal to what we've already seen.

## Code
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        i = 0
        substringHash = set()
        res = 0

        for j in range(len(s)):
            while s[j] in substringHash:
                substringHash.remove(s[i])
                i += 1
            substringHash.add(s[j])
            res = max(res, j - i + 1)

        return res
```

## Complexity
Time: O(n)
Space: O(n)
