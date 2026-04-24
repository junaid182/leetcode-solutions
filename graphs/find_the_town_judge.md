# Find the Town Judge

**Link:** https://leetcode.com/problems/find-the-town-judge/

## Approach

Model the trust relationships as a directed graph. The town judge must satisfy two conditions:
- Trusted by everyone else: **in-degree == n - 1**
- Trusts nobody: **out-degree == 0**

Track both counts in hashmaps as we iterate through the `trust` list. Then scan all people from `1` to `n` and return the one who meets both conditions. If none exists, return `-1`.

## Code

```python
class Solution:
    def findJudge(self, n: int, trust: List[List[int]]) -> int:
        incoming = defaultdict(int)
        outgoing = defaultdict(int)

        for src, dst in trust:
            incoming[dst] += 1
            outgoing[src] += 1
        
        for cur in range(1, n+1):
            if incoming[cur] == n-1 and outgoing[cur] == 0:
                return cur
        
        return -1
```

## Complexity

Time: O(E + n) — where E is the number of trust pairs, n is the scan at the end
Space: O(n) — hashmaps store at most n entries each
