# Permutation in String

**Link:** https://leetcode.com/problems/permutation-in-string/

## Approach

**Brute force:** Generate all permutations of s1 and check if any is a substring of s2. Exponential time.

**Optimized:** Fixed-size sliding window of length `len(s1)` over s2. Maintain a frequency map for s1 and a frequency map for the current window in s2. Slide the window one character at a time — add the new right character, remove the leftmost character when the window exceeds the target length. If both maps are equal at any point, a permutation exists.

**Why it works:** A permutation of s1 is just any arrangement of the same characters with the same frequencies. So instead of checking arrangements, we just compare frequency maps over a fixed-length window.

## Code

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        s1Hash = {}
        s2Hash = {}
        l = 0

        for c in s1:
            s1Hash[c] = s1Hash.get(c, 0) + 1
        
        for r in range(len(s2)):
            if r - l + 1 > len(s1):
                s2Hash[s2[l]] -= 1
                if s2Hash[s2[l]] == 0:
                    s2Hash.pop(s2[l])
                l += 1
            s2Hash[s2[r]] = s2Hash.get(s2[r], 0) + 1

            if s1Hash == s2Hash:
                return True

        return False
```

## Complexity

Time: O(n) — n is len(s2), window slides once through  
Space: O(1) — at most 26 characters in each frequency map
