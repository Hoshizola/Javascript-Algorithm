# leetcode415：字符串相加

给定两个字符串形式的非负整数 `num1` 和`num2` ，计算它们的和。

#### 方法一

这是最笨拙的办法。分别从两个字符串的最后一位开始遍历，设置一个`flag`变量表示进位数，取值为`0`或`1`。注意遍历完后还要判断最后有没有进位，如果有，要加到最前面。

```javascript
var addStrings = function(num1, num2) {
  let res = []
  let flag = false
  let i = num1.length - 1
  let j = num2.length - 1
  while(i >= 0 && j >= 0){
    let bitSum = parseInt(num1[i]) + parseInt(num2[j]) + (flag ? 1 : 0)
    if (bitSum > 9) {
      res.unshift(bitSum - 10)
      flag = true
    } else {
      res.unshift(bitSum)
      flag = false
    }
    i--
    j--
  }
  while(i >= 0) {
    let bitSum = parseInt(num1[i]) + (flag ? 1 : 0)
    if (bitSum > 9) {
      res.unshift(bitSum - 10)
      flag = true
    } else {
      res.unshift(bitSum)
      flag = false
    }
    i--
  }
  while(j >= 0) {
    let bitSum = parseInt(num2[j]) + (flag ? 1 : 0)
    if (bitSum > 9) {
      res.unshift(bitSum - 10)
      flag = true
    } else {
      res.unshift(bitSum)
      flag = false
    }
    j--
  }
  if(flag) {
    res.unshift(1)
  }
  return res.join('')
};
```

#### 方法二

思路没变，就是更精简了。若其中较短字符串遍历完了，将剩下的位数用`0`代替。

```javascript
var addStrings = function(num1, num2) {
  let res = []
  let i = num1.length - 1
  let j = num2.length - 1
  let flag = 0
  while(i >= 0 || j >= 0 || flag !== 0){
    let x = i >= 0 ? num1.charAt(i) - '0' : 0
    let y = j >= 0 ? num2.charAt(j) - '0' : 0
    let sum = x + y + flag
    res.unshift(sum % 10)
    flag = Math.floor(sum / 10)
    i--
    j--
  }
  return res.join('')
};
```





