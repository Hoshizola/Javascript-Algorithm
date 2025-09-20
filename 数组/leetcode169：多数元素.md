给定一个大小为 `n` 的数组 `nums` ，返回其中的多数元素。多数元素是指在数组中出现次数 **大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**示例 1：**

**输入：** nums = [3,2,3]
**输出：** 3

**示例 2：**

**输入：** nums = [2,2,1,1,1,2,2]
**输出：** 2

##### 题解
先遍历数组，记录每个数字出现的次数，再循环比较出现次数最大的那个元素
```javascript
var majorityElement = function(nums) {
    const countMap = new Map()
    for (let i = 0; i < nums.length; i++) {
        if (countMap.has(nums[i])) {
            countMap.set(nums[i], countMap.get(nums[i])+1)
        } else {
            countMap.set(nums[i], 1)
        }
    }

  
    let maxNum, maxCount = 0
    for(const [key, value] of countMap.entries()) {
        if (value > maxCount) {
            maxCount = value
            maxNum = key
        }
    }
    return maxNum

};
```