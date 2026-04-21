**In a town, there are n people labeled from 1 to n. There is a rumor that one of these people is secretly the town judge.**


**If the town judge exists, then:**

* **The town judge trusts nobody.**
* **Everybody (except for the town judge) trusts the town judge.**
* **There is exactly one person that satisfies properties 1 and 2.**
**You are given an array trust where trust[i] = [ai, bi] representing that the person labeled ai trusts the person labeled bi.**
**If a trust relationship does not exist in trust array, then such a trust relationship does not exist.**
https://leetcode.com/problems/find-the-town-judge/submissions/1984458336/
```swift
Return the label of the town judge if the town judge exists and can be identified, or return -1 otherwise.
```
 

**Example 1:**
```swift
Input: n = 2, trust = [[1,2]]
Output: 2
Example 2:

Input: n = 3, trust = [[1,3],[2,3]]
Output: 3
Example 3:

Input: n = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
```

**Constraints:**
```swift
1 <= n <= 1000
0 <= trust.length <= 104
trust[i].length == 2
All the pairs of trust are unique.
ai != bi
1 <= ai, bi <= n
```

**Solution**
```swift
class Solution {
    func findJudge(_ n: Int, _ trust: [[Int]]) -> Int {
        //
        var inDegree = Array(repeating: 0, count: n + 1)
        var outDegree = Array(repeating: 0, count: n + 1)

        for pair in trust {
            let a = pair[0]
            let b = pair[1]
            outDegree[a] += 1
            inDegree[b] += 1
        }

        for i in 1...n {
            //
            if inDegree[i] == n - 1 && outDegree[i] == 0 {
                return i
            }
        }
        return -1
    }
}
```
