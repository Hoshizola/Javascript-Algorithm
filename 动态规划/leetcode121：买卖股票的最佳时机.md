# leetcode121：买卖股票的最佳时机

给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。 

**示例 1：**

```tex
输入：[7,1,5,3,6,4]
输出：5
解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```

**示例 2：**

```tex
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 没有交易完成, 所以最大利润为 0。
```

#### 方法一：暴力法

对数组进行两重循环，找出最大的差值（本人在leetcode上实验显示超时，所以这种方法看看即可）

```javascript
var maxProfit = function(prices) {
    let len = prices.length
    let maxAns = 0
    for(let i = 0; i < len - 1; i++) {
        for(let j = i + 1; j < len; j++) {
            let diff = prices[j] - prices[i]
            maxAns = Math.max(diff, maxAns)
        }
    }
    return maxAns
}
```

#### 方法二：动态规划

可通过一次遍历，找出最大的那个利润差。在遍历时，记录目前为制遍历到的最小值`minPrice`，如果遍历到的数值比`minPrice`小，则更新`minPrice`的值，否则计算两者的差值，用变量`maxResult`维护着最大利润差，每次计算完差值后都需要跟`maxResult`比较，遍历完后返回`maxResult`。此过程只需`O(n)`的时间复杂度。

```javascript
var maxProfit = function(prices) {
  let minPrice = Infinity
  let maxResult = 0
  for(let i = 1, l = prices.length; i < l; i++) {
    if(prices[i] < minPrice) {
      minPrice = prices[i]
    }else {
      maxResult = Math.max(maxResult, prices[i] - minPrice)
    }
  }
  return maxResult
}
```

