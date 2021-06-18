# 剑指Offer 42：连续子数组的最大和

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

**示例1:**

输入: `nums = [-2,1,-3,4,-1,2,1,-5,4]`
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

#### 方法

- 创建一个新的数组`helper`，长度和原来的数组相同。遍历到哪个元素，`helper`对应位置就存放包含当前遍历元素的较大和。以上面例子来说，`helper[0]`就为-2，因为`-2+1=-1`小于`1`，所以遍历到第二个元素`1`时较大的和就是1，`helper[1]=1`，以此类推
- 因为在遍历过程中，`helper`只能存放包含当前元素的最大和，因此还需要用变量`maxResult`迭代一个全局的最大值

```javascript
var maxSubArray = function(nums) {
  let helper = new Array(nums.length)
  helper[0] = nums[0]
  let maxResult = nums[0]
  for(let i = 1, l = nums.length;i < l; i++) {
    helper[i] = Math.max(helper[i-1]+nums[i], nums[i])
    maxResult = Math.max(helper[i], maxResult)
  }
  return maxResult
}
```

