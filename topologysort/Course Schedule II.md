```swift
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.
```
 https://leetcode.com/problems/course-schedule-ii/



```swift
Example 1::

Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
```

```swift
Example 2:

Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
```
```swift
Example 3:

Input: numCourses = 1, prerequisites = []
Output: [0]
```

**Constraints:**
```swift
1 <= numCourses <= 2000
0 <= prerequisites.length <= numCourses * (numCourses - 1)
prerequisites[i].length == 2
0 <= ai, bi < numCourses
ai != bi
All the pairs [ai, bi] are distinct.
```

**Solution**
```swift
class Solution {
    func findOrder(_ numCourses: Int, _ prerequisites: [[Int]]) -> [Int] {
        //
        var graph: [[Int]] = Array(repeating: [Int](), count: numCourses)
        var inDegree: [Int] = Array(repeating: 0, count: numCourses)
        //
        for pair in prerequisites {
            let course = pair[0]
            let prerequisite = pair[1]
            graph[prerequisite].append(course)
            inDegree[course] += 1
        }
        var queue = [Int]()
        for index in 0..<numCourses {
            //
            if inDegree[index] == 0 {
                queue.append(index)
            }
        }
        //
        var result = [Int]()
        while(!queue.isEmpty) {
            let node = queue.removeFirst()
            result.append(node)
            for neibour in graph[node] {
                inDegree[neibour] -= 1
                if inDegree[neibour] == 0 {
                    queue.append(neibour)
                }
            }
        }
        return result.count == numCourses ? result : []
    }
}
```
