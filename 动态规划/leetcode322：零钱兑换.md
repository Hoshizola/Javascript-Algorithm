# leetcode322：零钱兑换

给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

你可以认为每种硬币的数量是无限的。

**示例 1：**

```tex 输入：coins = [1, 2, 5], amount = 11
输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
```

**示例 2：**

```tex 
输入：coins = [2], amount = 3
输出：-1
```

**示例 3：**

```tex
输入：coins = [1], amount = 0
输出：0
```

**示例 4：**

```tex
输入：coins = [1], amount = 1
输出：1
```

**示例 5：**

```tex
输入：coins = [1], amount = 2
输出：2
```

#### 动态规划思路

- 动态规划问题最重要的特征的就是具有最优子结构，针对这道题，我们要求凑到金额`amount`的最少硬币数，如果我们知道凑到金额`0~amount-1`的最少硬币数就容易了。

- 能求得凑到金额`0~amount-1`的最少硬币数，相当于子问题的最优问题已解决，而子问题又是怎么解决的呢？

  很明显，当金额为0时，方案数为0。以示例1为例，当金额为1时，遍历硬币数组，发现`1>=coins[0]`，可以将`coins[0]`加入，再遍历硬币数组，发现`1<coins[i](i>0)`，所以凑到金额1的最优解是选一个面值为1的硬币，记为`f(1)=1`；同理，`f(2)=1`，...，`f(11)`的值取决于`f(11-coins[0])`，`f(11-coins[1])`，`f(11-coins[2])`哪个值最小。

- 用一个数组记录`f(0)~f(amount)`的最优值，结果返回数组的最后一个数。

```javascript
var coinChange = function(coins, amount) {
  if(amount < 0) {
    return 0
  }
  let coinsLen = coins.length 
  let result = []
  // 第一个元素表示要凑到金额0有0种方案
  result.push(0)
  // 先把数组初始化为无穷大，便于后面的比较
  for(let i = 1; i <= amount; i++) {
    result.push(Infinity)
  }
  for(let i = 1; i <= amount; i++) {
    for(let j = 0; j < coinsLen; j++) {
      if(i >= coins[j]) {
        result[i] = Math.min(result[i], result[i-coins[j]] + 1)
      }
    }
  }
  // result[amount] > amount 说明没有方案
  // 因为result[amount] = Infinity，result[amount] > amount说明result[amount]没有被修改过
  return result[amount] > amount ? -1 : result[amount]
}
```



