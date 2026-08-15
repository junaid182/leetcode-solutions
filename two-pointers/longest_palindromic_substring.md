# Longest Palindromic Substring

**Link:** https://leetcode.com/problems/longest-palindromic-substring/

## Approach

Expand around center for every index. Each position is tried twice — once as the center of an odd-length palindrome (`l = r = i`) and once as the left center of an even-length palindrome (`l = i, r = i+1`). Expand outward while characters match, tracking the longest result found.

## Code

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ""
        resLen = 0

        def checkLongestPalindrome(l, r):
            nonlocal res, resLen
            while l >= 0 and r < len(s) and s[l] == s[r]:
                if r - l + 1 > resLen:
                    res = s[l:r+1]
                    resLen = r - l + 1
                
                l -= 1
                r += 1

        for i in range(len(s)):
            # check for odd numbers
            l, r = i, i
            checkLongestPalindrome(l, r)

            #check for even numbers
            l, r = i, i + 1
            checkLongestPalindrome(l, r)
        
        return res
```

## Complexity

Time: O(n²) — n centers, each expanding up to O(n)  
Space: O(1) — no extra space beyond the result
