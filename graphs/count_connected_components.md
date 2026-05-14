# Count Connected Components in an Undirected Graph

**Link:** https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/

## Approach

Build an undirected adjacency list. Iterate over all nodes — each unvisited node starts a new component. DFS from it to mark the entire connected component as visited.

## Code

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        adjMap = {i: [] for i in range(n)}

        for a, b in edges:
            adjMap[a].append(b)
            adjMap[b].append(a)
        
        visit = set()
        def dfs(node):
            if node in visit:
                return

            visit.add(node)

            for n in adjMap[node]:
                dfs(n)

        component = 0
        for i in range(n):
            if i not in visit:
                component += 1
                dfs(i)
        
        return component
```

## Complexity

Time: O(V + E) — each node and edge visited once  
Space: O(V + E) — adjacency list and visit set
