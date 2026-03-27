# Diameter of Binary Tree

**Link:** https://leetcode.com/problems/diameter-of-binary-tree/

## Approach

**Brute force:** For each node, compute the height of its left and right subtrees and sum them as the diameter through that node. Repeat for every node. This is O(n²) because height is recomputed from scratch at each node.

**Optimized:** Run a single DFS that computes height bottom-up. At each node, the diameter passing through it is `leftHeight + rightHeight`. Track the global maximum in a variable updated during the recursion, then return `1 + max(leftHeight, rightHeight)` as the height to the parent.

**Why it works:** The longest path in a binary tree must pass through some node as its highest point. At that node, the path length equals the height of the left subtree plus the height of the right subtree. By computing heights in a single DFS and recording the max diameter seen at every node, we find the answer in one pass.

## Code

```python
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        maxDia = 0

        def height(node):
            nonlocal maxDia

            if not node:
                return 0

            leftHeight = height(node.left)
            rightHeight = height(node.right)

            maxDia = max(maxDia, leftHeight + rightHeight)

            return 1 + max(leftHeight, rightHeight)

        height(root)

        return maxDia
```

## Complexity

Time: O(n) — every node is visited once
Space: O(n) — call stack depth is O(h); O(n) worst case for a skewed tree
