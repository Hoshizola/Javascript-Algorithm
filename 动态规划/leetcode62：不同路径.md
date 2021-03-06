# leetcode62：不同路径

一个机器人位于一个 `m x n` 网格的左上角，机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角，问总共有多少条不同的路径？

#### 思路

- 用一个dp表记录到达每个格子的路径数，要求得到达某个格子的路径，那么我们应该明确，机器人是如何到达这个格子的，根据题意，机器人只能从上方走下来或从左边走下来，因此，可以知道，到达一个格子的路径数等于到达上方格子的路径数加上到达左方格子的路径数
- 显然，到达网格的第一行的格子和第一列的格子都只有一种方法
- 整个算法的过程就是补全dp表的过程，dp表的最后一个格子填上后，说明已经求出答案

```javascript
var uniquePaths = function(m, n) {
  let dp = new Array(m).fill(0).map(item => new Array(n).fill(0))
  // dp表第一行
  for(let i = 1; i < n; i++) {
    dp[0][i] = 1
  }
  // dp表第一列
  for(let j = 1; j < m; j++) {
    dp[j][0] = 1
  }
  for(let i = 1; i < m; i++) {
    for(let j = 1; j < n; j++) {
      dp[i][j] = dp[i-1][j] + dp[i][j-1]
    }
  }
  return dp[m-1][n-1]
}
```

