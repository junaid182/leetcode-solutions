# Longest Common Prefix

**Link:** https://leetcode.com/problems/longest-common-prefix/

## Approach

**Brute force:** Compare every string against every other string character by character, tracking the shortest match. O(n²) comparisons.

**Optimized:** Use the first string as the reference. Scan it character by character (vertical scan). At each position `i`, check that character against every other string — if any string ends or differs at `i`, the prefix is done.

**Why it works:** The common prefix can be at most as long as the shortest string. By scanning vertically (column by column across all strings), the moment any string breaks the match we return immediately — no wasted work.

## Code

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        res = []

        for i in range(len(strs[0])):
            cur_char = strs[0][i]
            for s in strs:
                if i >= len(s) or s[i] != cur_char:
                    return "".join(res)
            res.append(cur_char)

        return "".join(res)
```

## Complexity

Time: O(n * m) — n is number of strings, m is length of the shortest string
Space: O(m) — result string grows up to length of the common prefix
