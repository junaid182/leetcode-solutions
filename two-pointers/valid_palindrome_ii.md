# Valid Palindrome II

**Link:** https://leetcode.com/problems/valid-palindrome-ii/

## Approach

**Brute force:** Try deleting each character one at a time and check if the result is a palindrome. O(n²) time.

**Optimized:** Two pointers from both ends. When a mismatch is found, we have exactly one deletion to use — try skipping the left character or the right character, and check if either remaining range is a palindrome.

**Why it works:** We only reach a mismatch at the first point where the string diverges from being a palindrome. At that point, one of the two characters must be the one to delete. If neither sub-range is a palindrome, no single deletion can fix it.

## Code

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1

        while l < r:
            if s[l] != s[r]:
                return self.isPalindrome(s, l+1, r) or self.isPalindrome(s, l, r - 1)

            l += 1
            r -= 1

        return True

    def isPalindrome(self, s, l, r):
        while l < r:
            if s[l] != s[r]:
                return False

            l += 1
            r -= 1

        return True
```

## Complexity

Time: O(n) — outer pass is O(n), helper checks at most O(n) more
Space: O(1) — no extra space used
