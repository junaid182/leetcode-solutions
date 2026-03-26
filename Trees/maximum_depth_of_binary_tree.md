# Maximum Depth of Binary Tree

**Link:** https://leetcode.com/problems/maximum-depth-of-binary-tree/

## Approach

**Brute force:** BFS level-order traversal, counting levels until the queue is empty. Works but requires O(n) extra space for the queue.

**Optimized:** Recursively compute the depth of the left and right subtrees, then return `1 + max(left, right)` at each node.

**Why it works:** The depth of any node is one more than the deeper of its two subtrees. The base case (null node) returns 0, so leaf nodes correctly return 1, and the max propagates back up to the root.

## Code

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        leftDepth = self.maxDepth(root.left)
        rightDepth = self.maxDepth(root.right)

        return 1 + max(leftDepth, rightDepth)
```

## Complexity

Time: O(n) — every node is visited once
Space: O(n) — call stack depth is O(h) where h is tree height; O(n) worst case for a skewed tree
