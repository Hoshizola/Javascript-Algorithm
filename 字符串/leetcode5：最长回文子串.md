# leetcode5：最长回文子串

给你一个字符串 s，找到 s 中最长的回文子串。

**示例 1：**

输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。

**示例 2：**

输入：s = "cbbd"
输出："bb"

**示例 3：**

输入：s = "a"
输出："a"

**示例 4：**

输入：s = "ac"
输出："a"

#### 方法一：暴力法

遍历所有可能的子串，判断每个子串是否是回文子串，如果是，记录当前回文子串的最大长度和子串开始的下标。

```javascript
var longestPalindrome = function(s) {
  let len = s.length
  let maxLen = 1, index = 0
  for(let i = 0; i < len - 1; i++) {
    for(let j = i + 1; j < len ; j++) {
      if(j - i + 1 > maxLen && isPalindrome(s.substring(i, j + 1))) {
        maxLen = j - i + 1
        index = i
      }
    }
  }
  return s.substr(index, maxLen)
}
// 定义判断回文子串的方法
var isPalindrome = function(str) {
  let len = str.length
  let left = 0
  let right = len - 1
  while(left < right) {
    if(str[left] !== str[right]) {
      return false
    }
    left++
    right--
  }
  return true
}
```

#### 方法二：动态规划

1、可以从子串长度为1开始遍历，直到子串等于原来字符串，判断每一种长度的子串是否是回文。

2、用动态规划判断回文，需要先建立一个二维dp表，记录左下标`i`到右下标`j`的子串是否是回文。判断回文的规则如下：

​	a)长度为1，一定是回文串；

​	b)长度为2或3，判断首尾字符是否相同，相同的就是回文串；

​	c)长度大于3，判断首尾字符是否相同并且包裹在左右下标中的子串是否是回文；

3、遍历过程中，更新遍历到的最长回文子串，遍历结束，直接将结果返回。

```javascript
var longestPalindrome = function(s) {
  // 创建二维dp表
  let sArr = new Array(s.length).fill(false).map(item => new Array(s.length).fill(false))
  let result = ''
  // l表示左下标到右下标的长度
  for(let l = 0; l < s.length; l++) {
    for(let i = 0; i + l < s.length; i++) {
      let j = i + l
      if(l === 0) {
        sArr[i][j] = true
      }else if(l === 1 || l === 2) {
        sArr[i][j] = (s[i] === s[j])
      }else {
        sArr[i][j] = sArr[i+1][j-1] && s[i] === s[j]
      }
      if(sArr[i][j] && l + 1 > result.length){
        result = s.substring(i, i + l + 1)
      }
    }
  }
  return result
};
```

#### 方法三：中心扩展法

1、遍历字符串中的每个字符，以长度为1或2的子串为中心，像左右两边扩散，如果字符相同，则继续向两边扩散，直到左右下标到达边界；

2、以长度为2的子串为中心扩散时，需要先判断两个字符是否相同，若不相同，无需扩散，直接返回1

```javascript
var longestPalindrome = function(s) {
  let len = s.length
  if(len === 0) {
    return ''
  }
  let maxLen = 0, index = 0
  for(let i = 0; i < len; i++) {
    let len1 = expand(s, i, i)
    let len2 = expand(s, i, i + 1)
    let longerLen = Math.max(len1, len2)
    if(longerLen > maxLen) {
      maxLen = longerLen
      index = i - Math.floor((maxLen-1)/2)
    }
  }
  return s.substr(index, maxLen)
}
// 扩散过程中的最长回文串长度
function expand(str, left, right) {
  if(str[left] !== str[right]) {
    return 1
  }
  let len = str.length
  while(left >= 0 && right < len && str[left] === str[right]) {
    left--
    right++
  }
  return right - left - 1
}
```

