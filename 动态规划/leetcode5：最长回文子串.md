# leetcode5：最长回文子串

给你一个字符串 s，找到 s 中最长的回文子串。

#### 方法：动态规划

1、可以从子串长度为1开始遍历，再遍历长度为2的子串，直到子串等于原来字符串，判断每一种长度的子串是否是回文。

2、用动态规划判断回文，需要先建立一个二维dp表，记录左下标`i`到右下标`j`的子串是否是回文。判断回文的规则如下：

​	a)长度为1，一定是回文串；

​	b)长度为2或3，判断首尾字符是否相同，相同的就是回文串；

​	c)长度大于3，判断首尾字符是否相同并且包裹在左右下标中的子串是否是回文；

3、遍历过程中，更新遍历到的最长回文子串，遍历结束，直接将结果返回。

```javascript
var longestPalindrome = function(s) {
  let len = s.length
  let dp = new Array(len).fill(false).map(item => new Array(len).fill(false))
  let result = ''
  for(let l = 0; l < len; l++) {
    for(let i = 0; i + l < len; i++){
      let j = i + l
      if(i === j) {
        dp[i][j] = true
      }else if(l === 1 || l === 2) {
        dp[i][j] = (s[i] === s[j])
      }else {
        dp[i][j] = (s[i] === s[j] && dp[i+1][j-1])
      }
      if(j - i + 1 > result.length && dp[i][j]) {
        result = s.substring(i, j+1)
      }
    }
  }
  return result
}
```

