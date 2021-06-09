# 只出现一次的数字Ⅲ

给定一个整数数组 `nums`，其中恰好有两个元素只出现一次，其余所有元素均出现两次。 找出只出现一次的那两个元素。你可以按 **任意顺序** 返回答案。

**示例 1：**

输入：`nums `= [1,2,1,3,2,5]
输出：[3,5]
解释：[5, 3] 也是有效的答案。

**示例 2：**

输入：`nums` = [-1,0]
输出：[-1,0]

**示例 3：**

输入：`nums` = [0,1]
输出：[1,0]

##### 方法一

1、将数组按从小到大排序，并创建一个哈希表

2、在遍历数组的过程中，如果哈希表中不存在该元素，则加入哈希表；

3、如果已存在，就再从哈希表中删除，这样就可以抵消出现两次的元素

4、最后存在在哈希表中的元素就是只出现一次的两个元素

```javascript
var singleNumber = function(nums) {
  nums.sort((a, b) => a - b)
  let map = new Map()
  for(let i = 0, len = nums.length; i < len; i++) {
    if(map.has(nums[i])) {
      map.delete(nums[i])
    }else {
      map.set(nums[i], i)
    }
  }
  let res = []
  for(let item of map.keys()) {
    res.push(item)
  }
  return res
};
```

