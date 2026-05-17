# Word Break

**Link:** https://leetcode.com/problems/word-break/

## Approach

Bottom-up DP from the end of the string. `dp[i]` is `True` if `s[i:]` can be segmented using `wordDict`. Base case: `dp[len(s)] = True` (empty suffix is always valid).

For each index `i`, try every word — if it matches `s[i:i+len(w)]` and `dp[i+len(w)]` is `True`, mark `dp[i] = True` and break early.

## Code

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * (len(s)+1)
        dp[len(s)] = True

        for i in range(len(s)-1, -1, -1):
            for w in wordDict:
                if (i + len(w)) <= len(s) and s[i:i+len(w)] == w:
                    dp[i] = dp[i+len(w)]
                if dp[i]:
                    break
        
        return dp[0]
```

## Complexity

Time: O(n × m × w) — n positions, m words, w max word length for slicing  
Space: O(n) — dp array
