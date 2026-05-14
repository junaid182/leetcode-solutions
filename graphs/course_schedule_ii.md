# Course Schedule II

**Link:** https://leetcode.com/problems/course-schedule-ii/

## Approach

Same cycle-detection DFS as Course Schedule, with two sets instead of one: `cycle` tracks the current DFS path (for cycle detection), `visit` marks fully processed courses. When a course's entire prerequisite chain resolves without a cycle, add it to `output` — this produces a valid topological order.

**Why it works:** Appending after all prerequisites are resolved ensures dependencies come before dependents. If a cycle is detected, return `[]`.

## Code

```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        preMap = {i: [] for i in range(numCourses)}
        for crs, pre in prerequisites:
            preMap[crs].append(pre)

        output = []

        visit, cycle = set(), set()
        def dfs(crs):
            if crs in cycle:
                return False
            if crs in visit:
                return True
            
            cycle.add(crs)
            for pre in preMap[crs]:
                if not dfs(pre): return False
            cycle.remove(crs)
            visit.add(crs)
            output.append(crs)

            return True
        
        for crs in range(numCourses):
            if not dfs(crs): return []
        
        return output
```

## Complexity

Time: O(V + E) — each course and prerequisite edge visited once  
Space: O(V + E) — adjacency list, two sets, and recursion stack
