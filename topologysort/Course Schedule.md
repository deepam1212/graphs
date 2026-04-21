```swift
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.
```
 https://leetcode.com/problems/course-schedule/description/



**Example 1:**
```swift
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true

Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**
```swift
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```
**Constraints:**
```swift
1 <= numCourses <= 2000
0 <= prerequisites.length <= 5000
prerequisites[i].length == 2
0 <= ai, bi < numCourses
All the pairs prerequisites[i] are unique.
```
**Solution**
```swift
class Solution {
    func canFinish(_ numCourses: Int, _ prerequisites: [[Int]]) -> Bool {
        //
        var graph: [[Int]] = Array(repeating: [Int](), count: numCourses)
        var inDegree: [Int] = Array(repeating: 0, count: numCourses)
        for pair in prerequisites {
            let course = pair[0]
            let prerequisite = pair[1]
            graph[prerequisite].append(course)
            inDegree[course] += 1
        }
        var queue = [Int]()
        for i in 0..<numCourses {
            if inDegree[i] == 0 {
                queue.append(i)
            }
        }
        var result: [Int] = [Int]()
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
        return result.count == numCourses
    }
}
```
