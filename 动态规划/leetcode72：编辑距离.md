#动态规划 

给你两个单词 `word1` 和 `word2`， _请返回将 `word1` 转换成 `word2` 所使用的最少操作数_  。

你可以对一个单词进行如下三种操作：

- 插入一个字符
- 删除一个字符
- 替换一个字符

**示例 1：**

**输入：** `word1 = "horse", word2 = "ros"`
**输出：** 3
**解释：**
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')

**示例 2：**

**输入：** `word1 = "intention", word2 = "execution"`
**输出：** 5
**解释：**
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')

##### 思路
`dp[i][j] `代表 word1 到 i 位置转换成 word2 到 j 位置需要最少步数

所以，

当 `word1[i] == word2[j]，dp[i][j] = dp[i-1][j-1]`；

当 `word1[i] != word2[j]，dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1`

其中，`dp[i-1][j-1]` 表示替换操作，`dp[i-1][j]` 表示删除操作，`dp[i][j-1]` 表示插入操作。

解释下为什么`dp[i-1,j]`到`dp[i,j]`是对应的删除操作，而`dp[i,j-1]`到`dp[i,j]`对应的是插入操作。

首先必须明确的是`dp[i,j]`表示的是： 源字符串前i个字符，变成和目标字符串前j个字符一模一样需要的编辑次数。

那么已知`dp[i-1,j]=n`，求`dp[i,j]`，意思是：已知原字符串前i-1个字符通过n次编辑可以和目标字符串前j个字符一模一样。求求`dp[i,j]`。

现在原字符串前进一位从i-1跑到i，这时要和目标字符串前j个字符一样，那么必须对跑到位置i的源字符串做一次删除操作，才能使得源字符串退回到i-i位置，这时他俩才能又一模一样。

##### 代码
```javascript
var minDistance = function(word1, word2) {
    const len1 = word1.length
    const len2 = word2.length
    const dp = new Array(len1 + 1).fill(0).map(() => new Array(len2 + 1).fill(0))
   // 初始化第0行
    for(let i = 0; i <= len2; i++) {
        dp[0][i] = i
    }
    // 初始化第0列
    for(let i = 0; i <= len1; i++) {
        dp[i][0] = i
    }
    for(let i = 1; i <= len1; i++) {
        for(let j = 1; j <= len2; j++) {
            if (word1[i - 1] !== word2[j-1]) {
                const up_left = dp[i-1][j-1] // 左上角，表示替换操作
                const up = dp[i-1][j] // 取上边，表示删除操作
                const left = dp[i][j-1] // 取左边，表示插入操作
                dp[i][j] = Math.min(up_left, up, left) + 1
            } else {
                dp[i][j] = dp[i - 1][j - 1]
            }
        }
    }
    return dp[len1][len2]
}
```
