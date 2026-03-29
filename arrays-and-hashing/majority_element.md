# Majority Element

**Link:** https://leetcode.com/problems/majority-element/

## Approach

**Brute force:** Count occurrences of each element with a hashmap, return the one with count > n/2. O(n) time, O(n) space.

**Optimized:** Boyer-Moore Voting Algorithm. Maintain a candidate and a count. For each number — if count is 0, set the current number as the new candidate. If the number matches the candidate, increment count; otherwise decrement. The majority element always survives because it appears more than all others combined.

**Why it works:** Every non-majority element can "cancel out" one majority element. Since the majority element appears > n/2 times, it can never be fully cancelled — it will always be the last candidate standing.

## Code

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        res = nums[0]
        count = 0

        for n in nums:
            if n == res:
                count += 1
            elif count == 0:
                res = n
                count += 1
            else:
                count -= 1

        return res
```

## Complexity

Time: O(n)
Space: O(1)
