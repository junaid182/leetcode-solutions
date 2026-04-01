# Group Anagrams

**Link:** https://leetcode.com/problems/group-anagrams/

## Approach

**Brute force:** Sort each string and use the sorted version as a key to group anagrams. O(n * k log k) time where k is the average string length.

**Optimized:** Instead of sorting, build a character frequency count of 26 integers for each string and use it as the hashmap key. This avoids the log factor from sorting.

**Why it works:** Any two anagrams will produce the exact same frequency array. Using `tuple(count)` makes it hashable so it can serve as a dictionary key, grouping all anagrams together.

## Code

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list)

        for s in strs:
            count = [0] * 26

            for c in s:
                count[ord(c) - ord("a")] += 1

            res[tuple(count)].append(s)

        return list(res.values())
```

## Complexity

Time: O(n * k) — n strings each of average length k
Space: O(n * k) — storing all strings in the hashmap
