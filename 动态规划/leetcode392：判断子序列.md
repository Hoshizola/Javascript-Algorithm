# leetcode392：判断子序列

给定字符串 s 和 t ，判断 s 是否为 t 的子序列。

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，"ace"是"abcde"的一个子序列，而"aec"不是）。

**示例 1：**

输入：s = "abc", t = "ahbgdc"
输出：true

**示例 2：**

输入：s = "axc", t = "ahbgdc"
输出：false

#### 方法一：双指针

- 用两个指针`sindex`和`tindex`分别指向s和t初始位置，遍历s和t，比较`sindex`位置和`tindex`位置是否相同，如果相同，`sindex`和`tindex`指向下一个，如果不相同，`tindex`指向下一个
- 若能遍历完s字符串，说明s包含在t中

```javascript
var isSubsequence = function(s, t) {
  let sindex = 0, tindex = 0
  let slen = s.length, tlen = t.length
  while(sindex < slen && tindex < tlen) {
    if(s[sindex] === tindex[j]) {
      sindex++
    }
    tindex++
  }
  return sindex === slen
}
```

#### 方法二：动态规划

- 用`dp[i][j]`表示字符串t的前`j`个字符包含`s`的前`i`个字符，所以递推公式是
  - 若`s[i-1]===t[j-1]`，则`dp[i][j]===dp[i-1][j-1]`
  - 若`s[i-1]!==t[j-1]`，则`dp[i][j]===dp[i][j-1]`

- 讨论边界条件，当`s`为空时，默认`t`包含`s`，返回`true`

```javascript
var isSubsequence = function(s, t) {
  let slen = s.length
  let tlen = t.length
  if(s === '') {
    return true
  }
  let dp = new Array(slen+1).fill(false).map(item => new Array(tlen+1).fill(false))
  // 边界条件
  for(let i = 0; i < tlen; i++) {
    dp[0][i] = true
  }
  for(let i = 1; i <= slen ; i++) {
    for(let j = 1; j <= tlen; j++) {
      // 递推公式
      if(s[i-1] === t[j-1]) {
        dp[i][j] = dp[i-1][j-1]
      }else {
        dp[i][j] = dp[i][j-1]
      }
    }
  }
  return dp[slen][tlen]
}
```

