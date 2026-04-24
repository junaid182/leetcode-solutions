# Verifying an Alien Dictionary

**Link:** https://leetcode.com/problems/verifying-an-alien-dictionary/

## Approach

Build a hashmap from the alien `order` string mapping each character to its index (its "rank"). Then check every adjacent pair of words.

For each pair, walk character by character until finding a difference:
- If `w1` runs out of characters while `w2` still has more, the pair is valid — continue.
- If `w2` runs out first (`j == len(w2)`), then `w1` is longer and has `w2` as a prefix, which violates order — return `False`.
- On the first differing character, compare their ranks. If `w1`'s character ranks higher than `w2`'s, return `False`. Otherwise `break` — no need to check further characters in this pair.

If all adjacent pairs pass, return `True`.

## Code

```python
class Solution:
    def isAlienSorted(self, words: List[str], order: str) -> bool:

        orderInd = {c: i for i, c in enumerate(order)}

        for i in range(len(words)-1):
            w1, w2 = words[i], words[i+1]

            for j in range(len(w1)):
                if j == len(w2):
                    return False
                
                if w1[j] != w2[j]:
                    if orderInd[w1[j]] > orderInd[w2[j]]:
                        return False
                    break
        
        return True
```

## Complexity

Time: O(M) — where M is the total number of characters across all words
Space: O(1) — the hashmap is always size 26
