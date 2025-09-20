给定一个未排序的整数数组 `nums` ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

请你设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

**示例 1：**

**输入：** nums = [100,4,200,1,3,2]
**输出：** 4
**解释：** 最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。

**示例 2：**

**输入：** nums = [0,3,7,2,5,8,4,6,0,1]
**输出：** 9

**示例 3：**

**输入：** nums = [1,0,1,2]
**输出：** 3

**题解**

按照题目要求，我们先找出起始的第一个数字，也就是[100, 200, 1]， 然后从这三个数字分别开始向后遍历，对比谁的长度最长，就是答案。

1、那么如何找出起始的第一个数字呢？第一个数字有什么特点呢？

- 第一个数字不存在前置数字，示例中，3 前面有 2，2 前面有 1 ，但是 1 前面没有任何数字了，所以 1 是第一个数字，同理 100，200 前面也都没有任何数字了，所以起始的第一个数字就有 [100, 200, 1]。

2、 找出来第一个数字了，接下来就只需要分别遍历这些起始数字，记录每一个数字连续长度。

- 1 后面有2，3，4，所以长度是4
- 100后面没有数字，长度是1
- 200后面没有数字，长度是1
- 对比每一个数字的连续长度，找出最长的那个。

#### 代码
###### 方法一（用数组会超时）
```javascript
var longestConsecutive = function(nums) {
    const numsArr = Array.from(new Set(nums))
    const firstNums = numsArr.filter(i => !numsArr.includes(i-1))
    const lengthArr = firstNums.map(i => {
        let n = 1
        while(numsArr.includes(i+n)) {
            n++
        }
        return n
    })

    return lengthArr.reduce((res, n) => Math.max(res, n), 0)

}
```
###### 方法二（改用Set）
```javascript
var longestConsecutive = function(nums) {
    const nums_set = new Set(nums)
    const firstNums = Array.from(nums_set).filter(i => !nums_set.has(i-1))
    const lengthArr = firstNums.map(i => {
        let n = 1
        while(nums_set.has(i+n)) {
            n++
        }
        return n
    })

    return lengthArr.reduce((res, n) => Math.max(res, n), 0)
}
```
