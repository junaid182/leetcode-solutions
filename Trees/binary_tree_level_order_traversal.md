# Binary Tree Level Order Traversal

**Link:** https://leetcode.com/problems/binary-tree-level-order-traversal/

## Approach

**Brute force:** DFS with a depth parameter, appending each node's value to the corresponding index in the result list. Works but BFS is more natural here.

**Optimized:** BFS using a queue. At the start of each iteration, snapshot the current queue length — that's exactly how many nodes belong to the current level. Process only that many nodes, appending their children for the next level.

**Why it works:** Snapshotting `len(q)` before the inner loop isolates each level. Children added during the loop won't be processed until the next iteration, so each `level` list contains exactly one depth's worth of nodes.

## Code

```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []

        q = collections.deque()
        q.append(root)

        while q:
            qLen = len(q)
            level = []
            for i in range(qLen):
                node = q.popleft()
                if node:
                    level.append(node.val)
                    q.append(node.left)
                    q.append(node.right)
            if level:
                res.append(level)

        return res
```

## Complexity

Time: O(n)  
Space: O(n)
