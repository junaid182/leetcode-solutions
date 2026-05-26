# Course Schedule II

**Link:** https://leetcode.com/problems/course-schedule-ii/

## Approach

Same cycle-detection DFS as Course Schedule, with two sets: `path` tracks the current DFS path (for cycle detection), `visited` marks fully processed courses. When a course's entire prerequisite chain resolves without a cycle, append it to `res` — this produces a valid topological order. Clearing `graph[crs]` after processing avoids redundant work.

**Why it works:** Appending after all prerequisites are resolved ensures dependencies come before dependents. If a cycle is detected, return `[]`.

## Code

```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        res = []
        graph = defaultdict(list)

        for course, pre in prerequisites:
            graph[course].append(pre)
        
        path = set()
        visited = set()
        def dfs(crs):
            if crs in path:
                return False
            
            if crs in visited:
                return True
            
            path.add(crs)
            for course in graph[crs]:
                if not dfs(course):
                    return False
            
            path.remove(crs)
            visited.add(crs)
            graph[crs] = []

            res.append(crs)

            return True

        for crs in range(numCourses):
            if not dfs(crs):
                return []
        
        return res
```

## Complexity

Time: O(V + E) — each course and prerequisite edge visited once  
Space: O(V + E) — adjacency list, two sets, and recursion stack
