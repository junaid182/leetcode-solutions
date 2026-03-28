# Valid Anagram

**Link:** https://leetcode.com/problems/valid-anagram/

## Approach

**Brute force:** Sort both strings and compare — O(n log n) time.

**Optimized:** Count character frequencies in both strings using hashmaps, then compare. Early exit if lengths differ.

**Why it works:** Two strings are anagrams if and only if they have identical character frequency counts. Building a map for each and comparing is a single-pass O(n) solution.

## Code

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:

        if len(s) != len(t):
            return False

        sMap = {}
        tMap = {}

        for c in s:
            sMap[c] = sMap.get(c, 0) + 1

        for c in t:
            tMap[c] = tMap.get(c, 0) + 1

        for key in sMap:
            if sMap[key] != tMap.get(key, 0):
                return False

        return True
```

## Complexity

Time: O(n)
Space: O(n)
