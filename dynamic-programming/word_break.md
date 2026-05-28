# Word Break

**Link:** https://leetcode.com/problems/word-break/

## Approach

Forward DP where `dp[i]` is `True` if `s[:i]` can be segmented using `wordDict`. Base case: `dp[0] = True` (empty prefix is always valid). Convert `wordDict` to a set for O(1) lookups.

For each endpoint `i`, check all start positions `j < i` — if `dp[j]` is `True` and `s[j:i]` is in the word set, mark `dp[i] = True` and break early.

## Code

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * (len(s)+1)
        dp[0] = True
        wordDict = set(wordDict)

        for i in range(1, len(s)+1):
            for j in range(len(s[:i])):
                if dp[j] and s[j:i] in wordDict:
                    dp[i] = True
                    break
        return dp[len(s)]
```

## Complexity

Time: O(n × m × w) — n positions, m words, w max word length for slicing  
Space: O(n) — dp array
