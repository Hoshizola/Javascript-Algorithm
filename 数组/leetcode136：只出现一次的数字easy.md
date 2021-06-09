# leetcode136：只出现一次的数字easy

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

**示例 1:**

输入: [2,2,1]
输出: 1

**示例 2:**

输入: [4,1,2,1,2]
输出: 4

##### 方法一

将数组按从小到大排序，相邻两个比较，如果不相等，则两个数中靠左的数字是答案，注意数组个数一定是奇数。

```javascript
var singleNumber = function(nums) {
  let len = nums.length
  let i
  nums.sort((a, b) => a - b)
  for(i = 0; i < len - 1; i+=2) {
    if(nums[i] !== nums[i+1]) {
      return nums[i]
    }
  }
  // 能执行到这里说明最后一个数是只出现一次的那个数
  if(i === len - 1) {
    return nums[len - 1]
  }
}
```

##### 方法二

异或法。两个相同的数由于其二进制数相同，异或结果一定为0，而只出现的那个数和0异或结果是其本身。因此可以将数组中全部的数进行异或运算，最终结果就是那个要求的只出现一次的数字。

```javascript
var singleNumber = function(nums) {
  return nums.reduce((prev, cur) => {
    return prev ^ cur
  })
}
```

