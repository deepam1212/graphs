**Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.**
**An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.**

 https://leetcode.com/problems/number-of-islands/submissions/1984475342/

**Example 1:**
```swift
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```
**Example 2:**
```swift
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

**Constraints:**
```swift
m == grid.length
n == grid[i].length
1 <= m, n <= 300
grid[i][j] is '0' or '1'.
```

**Solution**
```swift
class Solution {
    func numIslands(_ grid: [[Character]]) -> Int {
        //
        var grid = grid
        var rows: Int = grid.count
        var cols: Int = grid[0].count
        var islandCount: Int = 0
        for i in 0..<rows {
            for j in 0..<cols {
                if grid[i][j] == "1" {
                    islandCount += 1
                    dfs(&grid, i, j)
                }
            }
        }
        //
        return islandCount
    }

    func dfs(_ grid: inout [[Character]], _ i: Int, _ j: Int) {
        if i < 0 || j < 0 || i >= grid.count || j >= grid[0].count || grid[i][j] == "0" {
            return
        }
        grid[i][j] = "0"
        dfs(&grid, i + 1, j)
        dfs(&grid, i - 1, j)
        dfs(&grid, i, j + 1)
        dfs(&grid, i, j - 1)
    }
}
```
