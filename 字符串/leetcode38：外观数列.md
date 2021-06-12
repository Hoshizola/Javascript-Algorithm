# leetcode38：外观数列

给定一个正整数 n ，输出外观数列的第 n 项。

「外观数列」是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。

你可以将其视作是由递归公式定义的数字字符串序列：

    countAndSay(1) = "1"
    countAndSay(n) 是对 countAndSay(n-1) 的描述，然后转换成另一个数字字符串。

前五项如下：

```tex
1.1
2.11
3.21
4.1211
5.111221
第一项是数字 1 
描述前一项，这个数是 1 即 “ 一 个 1 ”，记作 "11"
描述前一项，这个数是 11 即 “ 二 个 1 ” ，记作 "21"
描述前一项，这个数是 21 即 “ 一 个 2 + 一 个 1 ” ，记作 "1211"
描述前一项，这个数是 1211 即 “ 一 个 1 + 一 个 2 + 二 个 1 ” ，记作 "111221"
```

#### 方法

1、题目已经提示`countAndSay(n)` 是对 `countAndSay(n-1) `的描述，因此要求`countAndSay(n)`，就需要先求出 `countAndSay(n-1) `，明显可以用递归的方法，而递归的终止条件是当`n=1`时，返回字符串`"1"`

2、得到 `countAndSay(n-1) `后，遍历该字符串，用变量`count`记录当前要统计的连续相同的字符个数，当遇到不同字符时，把统计到的描述结果拼接到变量`result`，遍历结束后将`result`返回

```javascript
var countAndSay = function(n) {
  if(n === 1) {
    return 1
  }
  let lastResult = countAndSay(n - 1)
  let len = lastResult.length 
  let index = 0
  let result = ''
  while(index < len) {
    let ch = lastResult[index]
    let count = 0
    while(index < len && lastResult[index] === ch) {
      index++
      count++
    }
    result += count + ch
  }
  return result
}
```

