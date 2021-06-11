# leetcode14：最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

**示例 1：**

输入：`strs = ["flower","flow","flight"]`
输出：`"fl"`

**示例 2：**

输入：`strs = ["dog","racecar","car"]`
输出：`""`
解释：输入不存在公共前缀。

#### 方法一

1、先判断字符串数组的长度是否为0，如果为0，说明数组中没有字符串，直接返回""；

2、如果数组长度不为0，先初始化公共前缀`prefix`是第一个字符串，从第二个字符串开始循环遍历，每遍历到一个元素都能先得到目前为止长度最长的公共前缀；

3、若在遍历过程中`prefix`已经是`""`，直接返回空字符串；否则返回`prefix`

```javascript
var longestCommonPrefix = function (strs) {
  if (!strs || strs.length === 0) {
    return ''
  }
  let len = strs.length
  let prefix = strs[0]
  for (let i = 1; i < len; i++) {
    prefix = longestCommonPrefixOfStr(prefix, strs[i])
    if (prefix === '') {
      return ''
    }
  }
  return prefix
}
// 求两个字符串的最长公共前缀
var longestCommonPrefixOfStr = function (str1, str2) {
  let l = 0
  let minLen = Math.min(str1.length, str2.length) 
  while(l < minLen && str1[l] === str2[l]) {
    l++
  }
  return str1.slice(0, l)
}
```

#### 方法二

1、先假设最长公共前缀的长度为1，且为第一个字符串的第一个字符，设置变量`i`，表示与第一个字符串的第`i`个字符进行匹配，初始化为0，并且设置一个标志位`flag`表示匹配是否正在进行，若`flag`为`false`，表示已经找到最长公共前缀，算法终止；

2、将第一个字符串的第`i`个字符与数组中其他所有字符串的第`i`个字符进行匹配，如果都相等，`i`加1；如果不相等，将`flag`设为`false`，并返回第一个字符串的前`i`个字符。

```javascript
var longestCommonPrefix = function (strs) {
  let len = strs.length
  if (!strs || len === 0) {
    return ''
  }
  let i = 0
  let flag = true
  while (flag) {
    if (i < strs[0].length) {
      let char = strs[0][i]
      for (let j = 1; j < len; j++) {
        if (strs[j].length < i || strs[j][i] !== char) {
          flag = false
          break
        }
      }
    }else {
      flag = false
    }
    i++
  }
  return strs[0].slice(0, i - 1)
}
```

