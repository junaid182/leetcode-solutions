# Longest Repeating Character Replacement

**Link:** https://leetcode.com/problems/longest-repeating-character-replacement/

## Approach

**Brute force:** Try every substring, count the most frequent character, and check if the remaining characters (those to replace) are <= k. O(n²) or O(n³).

**Optimized:** Sliding window. Maintain a frequency map of characters in the current window. The key insight is that a window is valid if `window_size - max_frequency <= k` — meaning we only need to replace the non-dominant characters. Expand the right pointer always; shrink the left pointer when the window becomes invalid. Track `maxf` (the highest frequency seen) globally — we never need to shrink `maxf` because a smaller window with a lower `maxf` can never beat our current best.

**Why it works:** At any point, the minimum replacements needed equals `window_size - max_frequency`. If that exceeds k, the window is invalid and we slide it forward. Since we want the longest window, we never shrink the window size — we just slide it.

## Code

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = {}
        l = 0
        longest = 0
        maxf = 0

        for r in range(len(s)):
            count[s[r]] = count.get(s[r], 0) + 1
            maxf = max(maxf, count[s[r]])

            if (r - l + 1) - maxf > k:
                count[s[l]] -= 1
                l += 1

            longest = max(longest, r - l + 1)
        
        return longest
```

## Complexity

Time: O(n)  
Space: O(1) — at most 26 characters in the frequency map
