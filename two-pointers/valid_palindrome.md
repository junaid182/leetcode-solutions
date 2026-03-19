# Valid Palindrome

**Link:** https://leetcode.com/problems/valid-palindrome/

## Approach

**Brute force:** Filter the string to only alphanumeric characters, lowercase it, then check if it equals its reverse. O(n) time but O(n) space for the filtered string.

**Optimized:** Two pointers from both ends. Skip non-alphanumeric characters on each side, then compare the characters case-insensitively. If any mismatch is found, return False. If the pointers meet, it's a palindrome.

**Why it works:** By skipping non-alphanumeric characters in-place, we avoid building a new string. Comparing from both ends simultaneously means we only need one pass through the string.

## Code

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1

        while l < r:
            while l < r and not s[l].isalnum():
                l += 1

            while l < r and not s[r].isalnum():
                r -= 1

            if s[l].lower() != s[r].lower():
                return False

            l += 1
            r -= 1

        return True
```

## Complexity

Time: O(n) — each character is visited at most once
Space: O(1) — no extra space, operates directly on the string
