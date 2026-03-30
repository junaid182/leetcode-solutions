# Best Time to Buy and Sell Stock

**Link:** https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

## Approach

**Brute force:** Try every pair of buy/sell days and track the maximum profit. O(n²) time.

**Optimized:** Sliding window with two pointers. Left pointer tracks the buy day, right pointer scans forward. If we find a higher price, update max profit. If we find a price lower than the buy day, shift the buy pointer to the current day since that's a better buy candidate.

**Why it works:** We only sell on days after we buy. Whenever we see a price lower than our current buy price, there's no reason to keep the old buy day — selling later from the new lower price will always yield more profit.

## Code

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        L = 0
        maxProfit = 0

        for R in range(len(prices)):
            maxProfit = max(maxProfit, prices[R] - prices[L])

            if prices[R] < prices[L]:
                L = R

        return maxProfit
```

## Complexity

Time: O(n) — single pass through prices
Space: O(1) — only two pointers and a max tracker
