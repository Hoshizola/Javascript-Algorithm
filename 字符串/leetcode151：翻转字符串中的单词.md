### leetcode151：翻转字符串中的单词

给定一个字符串，逐个翻转字符串中的每个单词。

**说明：**

1. 无空格字符构成一个 单词 
2. 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括
3. 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

**思路一：**

1. 先将去除字符串两边的空格
2. 以空格为分隔符转为数组
3. 去除长度为0，即空字符串的元素，反转再拼接

```javascript
var reverseWords = function(s) {
    let strArr = s.trim().split(' ')
    let result = []
    for(let i = 0; i < strArr.length; i++){
        if(strArr[i].length !== 0){ //多余的空格变成数组元素后长度为0，即空字符串
            result.push(strArr[i])
        }
    }
    return result.reverse().join(' ')
};
```

**思路二：**

1. 先去除字符串两端的空格
2. 利用正则表达式将单词中的空格全部替换成一个空格
3. 分割字符串，翻转，再拼接

```javascript
var reverseWords = function(s) {
    return s.trim().replace(/\s+/g, ' ').split(' ').reverse().join(' ')
};
```

