# Merge Strings Alternately

**Link:** https://leetcode.com/problems/merge-strings-alternately/

## Approach

**Brute force:** Build the result by iterating up to `max(len(word1), len(word2))` and appending characters one by one with bounds checks.

**Optimized:** Two pointers advancing together — append from both strings simultaneously while both have characters, then append the leftover tail of whichever string is longer.

**Why it works:** Both pointers always move in sync, so we never miss a character or duplicate one. Once one string is exhausted, the remaining slice of the other can be appended directly.

## Code

```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        p1, p2 = 0, 0
        res = []

        while p1 <= len(word1) - 1 and p2 <= len(word2) - 1:
            res.append(word1[p1])
            res.append(word2[p2])
            p1 += 1
            p2 += 1

        if p1 <= len(word1) - 1:
            res.append(word1[p1:])

        if p2 <= len(word2) - 1:
            res.append(word2[p2:])

        return "".join(res)
```

## Complexity

Time: O(n + m) — each character from both strings is visited once
Space: O(n + m) — result list holds all characters
