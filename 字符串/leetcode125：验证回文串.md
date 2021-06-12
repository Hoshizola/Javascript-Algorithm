# leetcode125：验证回文串

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例 1:**

输入: "A man, a plan, a canal: Panama"
输出: true

**示例 2:**

输入: "race a car"
输出: false

#### 方法一

1、先去除字符串两边的空格，再定义一个判断一个字符是否是字母或数字的方法；

2、采用双指针的方法，判断左指针所指字符是否是字母或数字，不是则跳过，指针继续右移，直到字符是字母或数字；右指针也进行同样的操作；

3、忽略大小写判断左右指针字符是否相同，不同直接返回`false`，相同则右（左）指针左（右）移

```javascript
var isPalindrome = function(s) {
  let str = s.trim()
  let left = 0, right = str.length - 1
  while(left < right) {
    if(!isNumOrAlpha(str[left]) && left < right) {
      left++
    }
    if(!isNumOrAlpha(str[right]) && left < right) {
      right--
    }
    if(str[left].toLowerCase() !== str[right].toLowerCase()) {
      return false
    }
    left++
    right--
  }
  return true
}
// 判断字符是否是字母或数字
function isNumOrAlpha(char) {
  return new RegExp(/^[0-9a-zA-Z]$/).test(char)
}
```

#### 方法二

1、定义一个数组，遍历字符串，把是字母或数字的字符加进数组中，为了忽略大小写，把所有字母都变成小写再加入；

2、将数组转为字符串后的结果和将数组翻转后再转为字符串的结果比较是否相同。

```javascript
var isPalindrome = function(s) {
  let new_sArr = []
  for(let i = 0, len = s.length; i < len; i++) {
    if(isNumOrAlpha(s[i])) {
      new_sArr.push(s[i].toLowerCase())
    }
  }
  return new_sArr.join('') === new_sArr.reverse().join('')
};
var isNumOrAlpha = function(s){
    return /^[a-zA-Z0-9]$/.test(s)
}
```

