# Lowest Common Ancestor of a Binary Search Tree

**Link:** https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

## Approach

**Brute force:** Record the path from root to p and from root to q, then find the last node they share. O(n) time and O(n) space for the paths.

**Optimized:** Exploit the BST property iteratively. At each node, if both p and q are greater, the LCA must be in the right subtree. If both are smaller, it's in the left subtree. Otherwise, the current node is the split point — meaning it is the LCA.

**Why it works:** In a BST, the LCA is exactly the first node where p and q stop being on the same side. That split point is where one value is ≤ cur and the other is ≥ cur, so returning `cur` at that moment is always correct.

## Code

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        cur = root

        while cur:
            if p.val > cur.val and q.val > cur.val:
                cur = cur.right
            elif p.val < cur.val and q.val < cur.val:
                cur = cur.left
            else:
                return cur
```

## Complexity

Time: O(h) where h is the height of the tree (O(log n) for balanced, O(n) worst case)  
Space: O(1)
