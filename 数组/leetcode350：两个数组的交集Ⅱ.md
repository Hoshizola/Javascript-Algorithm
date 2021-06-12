# leetcode350：两个数组的交集Ⅱ

给定两个数组，编写一个函数来计算它们的交集。

**示例 1：**

输入：`nums1 = [1,2,2,1], nums2 = [2,2]`
输出：`[2,2]`

**示例 2:**

输入：`nums1 = [4,9,5], nums2 = [9,4,9,8,4]`
输出：`[4,9]`

**说明：**

    输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
    我们可以不考虑输出结果的顺序。

#### 方法一

1、遍历第一个数组，将第一个数组的值、该值出现的次数，以`(key:value)`的形式存储下来

2、遍历第二个数组，判断是否在`(key:value)`中存在，存在则 `value` 减去 1，继续。

```javascript
var intersect = function(nums1, nums2) {
  let hashObject = {}
  for(let i = 0; i < nums1.length; i++) {
    if(hashObject[nums1[i]]) {
      hashObject[nums1[i]] += 1
    }else{
      hashObject[nums1[i]] = 1
    }
  }
  let res = []
  for(let i = 0; i <nums2.length; i++) {
    if(hashObject[nums2[i]] > 0) {
      res.push(nums2[i])
      hashObject[nums2[i]] -= 1
    }
  }
  return res
}
```

#### 方法二

用变量`shortArr`保存长度较短的数组，变量`longArr`保存长度较长的数组，遍历短数组，若长数组中也有，则将该元素加入`result`数组，并从长数组中删除

```javascript
var intersect = function(nums1, nums2) {
  let shortArr = nums1.length < nums1.length ? nums1 : nums2
  let longArr = nums1.length >= nums2.length ? nums1 : nums2
  let result = []
  for(let i = 0, l = shortArr.length; i < l; i++) {
    if(longArr.includes(shortArr[i])) {
      result.push(shortArr[i])
      longArr.splice(longArr.indexOf(shortArr[i]), 1)
    }
  }
  return result
}
```

