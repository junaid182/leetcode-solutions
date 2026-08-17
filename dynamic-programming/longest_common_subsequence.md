# Longest Common Subsequence

**Link:** https://leetcode.com/problems/longest-common-subsequence/

## Approach

Bottom-up DP on a 2D grid where `dp[r][c]` = length of LCS of `text1[r:]` and `text2[c:]`. Fill from bottom-right to top-left:
- If characters match: `dp[r][c] = 1 + dp[r+1][c+1]`
- Otherwise: `dp[r][c] = max(dp[r+1][c], dp[r][c+1])` — skip one character from either string

The answer is `dp[0][0]`.

## Code

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[0 for j in range(len(text2)+1)] for i in range(len(text1)+1)]

        for r in range(len(text1)-1, -1, -1):
            for c in range(len(text2)-1, -1, -1):
                if text1[r] == text2[c]:
                    dp[r][c] = 1 + dp[r+1][c+1]
                else:
                    dp[r][c] = max(dp[r+1][c], dp[r][c+1])
        
        return dp[0][0]
```

## Complexity

Time: O(m × n) — filling the entire DP grid  
Space: O(m × n) — 2D dp array
