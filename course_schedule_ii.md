## Course Schedule II (Imp)

- #### [Leetcode](https://leetcode.com/problems/course-schedule-ii/)
- #### [CodeStudio](https://www.codingninjas.com/codestudio/problems/course-schedule-ii_1069243)

### Problem Statement

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

### Solution

similar method to course schedule
instead just return topo-sorted nodes

### Code

```Python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        course_g = {i: [] for i in range(numCourses)}
        in_degree = [0]*numCourses
        for u, v in prerequisites:
            course_g[u].append(v)
            in_degree[v] += 1

        que = []
        for i in range(numCourses):
            if in_degree[i] == 0:
                que.append(i)
        topo = []
        while que:
            c = que.pop(0)
            topo.insert(0, c)

            for pre in course_g[c]:
                in_degree[pre]-=1
                if in_degree[pre] == 0:
                    que.append(pre)

        return topo if len(topo)==numCourses else []

```
