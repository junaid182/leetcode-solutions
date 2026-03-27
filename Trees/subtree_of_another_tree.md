# Subtree of Another Tree

**Link:** https://leetcode.com/problems/subtree-of-another-tree/

## Approach

**Brute force:** At every node in `root`, serialize the subtree rooted there and compare it to the serialized `subRoot`. O(n * m) time with extra space for serialization.

**Optimized:** At each node of `root`, check if the subtree rooted there is identical to `subRoot` using a `isSameTree` helper. If not, recurse into the left and right children. This reuses the Same Tree logic directly.

**Why it works:** A tree `s` is a subtree of `t` if and only if `s` is identical to `t`, or `s` is a subtree of `t`'s left child, or `s` is a subtree of `t`'s right child. The `isSameTree` check handles structural and value equality at each candidate root in one DFS pass.

## Code

```python
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root and not subRoot:
            return True

        if not root:
            return False

        if self.isSameTree(root, subRoot):
            return True

        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)

    def isSameTree(self, p, q):
        if not p and not q:
            return True

        if not p or not q:
            return False

        if p.val != q.val:
            return False

        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

## Complexity

Time: O(n * m) — for each of the n nodes in `root`, we may run isSameTree which is O(m) where m is the size of `subRoot`
Space: O(n) — call stack depth is O(h) for the outer recursion; O(n) worst case for a skewed tree
