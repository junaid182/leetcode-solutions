# Merge Strings Alternately

**Link:** https://leetcode.com/problems/merge-strings-alternately/

## Approach

**Brute force:** Zip the two strings together, append each pair of characters, then append whichever string has remaining characters. Same idea, just using Python's built-in `zip`.

**Optimized:** Two pointers advancing through both strings simultaneously. Append one character from each per iteration, then append the leftover tail of whichever string is longer.

**Why it works:** Since we process both strings in lockstep, we naturally alternate characters. Slicing the remainder after the loop handles unequal lengths cleanly without extra conditionals.

## Code

```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        res = []

        l, r = 0, 0

        while l < len(word1) and r < len(word2):
            res.append(word1[l])
            res.append(word2[r])
            l += 1
            r += 1

        res.append(word1[l:])
        res.append(word2[r:])

        return "".join(res)
```

## Complexity

Time: O(n + m) — where n and m are the lengths of word1 and word2
Space: O(n + m) — for the result list
