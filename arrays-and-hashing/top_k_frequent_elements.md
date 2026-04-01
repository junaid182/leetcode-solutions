# Top K Frequent Elements

**Link:** https://leetcode.com/problems/top-k-frequent-elements/

## Approach

**Brute force:** Count frequencies with a hashmap, then sort by frequency descending and return the first k elements. O(n log n) time.

**Optimized:** Bucket sort — create a frequency array where index represents count. Since no element can appear more than `len(nums)` times, the array size is bounded. Iterate from highest frequency down, collecting elements until we have k results.

**Why it works:** Frequency values are bounded by the input size, so we can use the frequency as an index. Iterating in reverse gives us the most frequent elements first without sorting.

## Code

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        countHash = {}
        freq = [[] for i in range(len(nums) + 1)]

        for n in nums:
            countHash[n] = countHash.get(n, 0) + 1

        for n, c in countHash.items():
            freq[c].append(n)

        res = []
        for f in range(len(freq) - 1, 0, -1):
            for n in freq[f]:
                res.append(n)
                if len(res) == k:
                    return res
```

## Complexity

Time: O(n) — counting is O(n), bucket sort is O(n)
Space: O(n) — hashmap and frequency array both scale with input size
