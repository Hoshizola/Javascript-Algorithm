';给你一个整数数组 `nums`，返回 数组 `answer` ，其中 `answer[i]` 等于 `nums` 中除 `nums[i]` 之外其余各元素的乘积 。

题目数据 **保证** 数组 `nums`之中任意元素的全部前缀元素和后缀的乘积都在  **32 位** 整数范围内。

请 **不要使用除法，** 且在 `O(n)` 时间复杂度内完成此题。

**示例 1:**

**输入:** nums = `[1,2,3,4]`
**输出:** `[24,12,8,6]`

**示例 2:**

**输入:** nums =` [-1,1,0,-3,3]`
**输出:** ` [0,0,9,0,0]`

**提示：**

- `2 <= nums.length <= 105`
- `-30 <= nums[i] <= 30`
- 输入 **保证** 数组 `answer[i]` 在  **32 位** 整数范围内

##### 方法一（使用了除法，没符合要求，也能解）

先统计数组中0的个数
- 如果数组中不存在0，先计算整个数组所有的乘积，再遍历数组过程中除掉当前数值
- 如果数组中存在一个0，在乘积结果数组中对应某个下标位置是其他非0数字的乘积，其余位置全部为0
- 如果数组存在2个或2个以上的0，整个结果数组为0

```javascript
var productExceptSelf = function(nums) {
    const zeroIndex = []
    // 统计数组中0的个数
    nums.forEach((item, index) => {
        if (item === 0) {
            zeroIndex.push(index)
        }
    })
    const zeroLength = zeroIndex.length
    let result = []
    if (zeroLength === 0) {
        const allMulti = nums.reduce((prev, item) => {
            return prev * item
        }, 1)
        nums.forEach(item => {
            result.push(allMulti / item)
        })

    } else if (zeroLength === 1) {
        result = new Array(nums.length).fill(0)
        result[zeroIndex[0]] = nums.reduce((prev, item) => {
            if (item !== 0) {
                return prev * item
            } else {
                return prev
            }
        }, 1)
    } else {
        result = new Array(nums.length).fill(0)
    }
    return result
}
console.log(productExceptSelf([-1,1,0,-3,3]))
```

##### 方法二（不用除法）

详解：[238. 除自身以外数组的乘积 - 力扣（LeetCode）](https://leetcode.cn/problems/product-of-array-except-self/solutions/2783788/qian-hou-zhui-fen-jie-fu-ti-dan-pythonja-86r1/?envType=study-plan-v2&envId=top-100-liked)


```javascript
var productExceptSelf = function(nums) {
    const len = nums.length
    const result = []
    const pre = new Array(len), after = new Array(len)
    pre[0] = 1, after[len - 1] = 1
    for(let i = 1; i < len; i++) {
        pre[i] = pre[i-1] * nums[i-1]
    }
    for(let i = len - 2; i >= 0; i--) {
        after[i] = after[i+1] * nums[i + 1]
    }
    for(let i = 0; i < nums.length; i++) {
        result[i] = pre[i] * after[i]
    }
    return result
}
```


