# leetcode746：使用最小花费爬楼梯

数组的每个下标作为一个阶梯，第 i 个阶梯对应着一个非负数的体力花费值 cost[i]（下标从 0 开始）。

每当你爬上一个阶梯你都要花费对应的体力值，一旦支付了相应的体力值，你就可以选择向上爬一个阶梯或者爬两个阶梯。

请你找出达到楼层顶部的最低花费。在开始时，你可以选择从下标为 0 或 1 的元素作为初始阶梯。

**示例 1：**

```tex 
输入：cost = [10, 15, 20]
输出：15
解释：最低花费是从 cost[1] 开始，然后走两步即可到阶梯顶，一共花费 15 。
```

 **示例 2：**

```tex 输入：cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
输出：6
解释：最低花费方式是从 cost[0] 开始，逐个经过那些 1 ，跳过 cost[3] ，一共花费 6 。
```

#### 动态规划思路

- 使用动态规划，需要用一个`dp`数组来记录状态，本题使用一个一维数组`dp[i]`，记录到达第`i`个阶梯的最小花费，可想而知，`dp[i]=Math.min(dp[i-1]+cost[i], dp[i-2]+cost[i])`。注意这里加的是`cost[i]`，因为题目中说明，这个值表示爬上这个阶梯要花费的体力值，也就是说，到达最顶阶梯时可以看作是不花费任何体力
- 初始化`dp[0]=cost[0]`，`dp[1]=cost[1]`，剩下的`dp`数组的值可以由这两个来推导
- 因为到达最顶阶梯时可以看作是不花费任何体力，所以结果取`dp`数组中倒数的两个数的最小值

```javascript
var minCostClimbingStairs = function(cost) {
  let len = cost.length
  if(len === 2) {
    return Math.min(cost[0], cost[1])
  }
  let dp = new Array(len)
  dp[0] = cost[0]
  dp[1] = cost[1]
  for(let i = 2; i < len; i++) {
    dp[i] = Math.min(dp[i-2]+cost[i], dp[i-1]+cost[i])
  }
  // 注意最后一步可以理解为不用花费，所以取倒数第一步或者倒数第二步
  return Math.min(dp[len-1], dp[len-2])
}