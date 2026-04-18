# Binary Tree Right Side View

**Link:** https://leetcode.com/problems/binary-tree-right-side-view/

## Approach

**Brute force:** DFS tracking depth, overwriting the result at each depth with the current node's value. The last write at each depth ends up being the rightmost node. Works but BFS is more intuitive.

**Optimized:** BFS level order traversal. For each level, track the last non-null node seen — that's the rightmost node visible from the right side.

**Why it works:** Processing nodes left-to-right within each level means the final non-null node encountered is always the rightmost. Snapshotting `qLen` isolates each level exactly as in standard level order traversal.

## Code

```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        queue = collections.deque()
        queue.append(root)
        res = []

        while queue:
            level = []
            for i in range(len(queue)):
                node = queue.popleft()
                if node:
                    level.append(node.val)
                    queue.append(node.left)
                    queue.append(node.right)
            if level:
                res.append(level[-1])

        return res
```

## Complexity

Time: O(n)  
Space: O(n)
