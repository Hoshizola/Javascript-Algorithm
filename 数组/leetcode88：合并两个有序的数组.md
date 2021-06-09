# leetcode88：合并两个有序的数组

题目描述：给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。你可以假设 nums1 的空间大小等于 m + n，这样它就有足够的空间保存来自 nums2 的元素。

**示例 1：**

输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]

**示例 2：**

输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]

##### 方法一

可以先将两个数组合并为一个数组，再排序

```javascript
var merge1 = function(nums1, m, nums2, n) {
  nums1.splice(m, n, ...nums2)
  nums1.sort((a,b) => a - b)
  return nums1
}
```

##### 方法二

逆向指针法。将一个指针`len1`指向`nums1`有效数字部分的末尾，将一个指针`len2`指向`nums2`数组的末尾，另外将一个指针`len`指向`nums1`整个数组的末尾。若`len2`指向的数字比`len1`大，则将前者填入`len`指向的位置，`len`指针向前移。反之亦然。

```javascript
var merge = function(nums1, m, nums2, n) {
  let len = m + n - 1
  let len1 = m - 1
  let len2 = n - 1
  while(len2 >= 0) {
    nums1[len--] = nums1[len1] >= nums2[len2] ? nums1[len1--] : nums2[len2--]
    if(len1 < 0) {
      nums1[len--] = nums2[len2--]
      continue
    }
  }
  return nums1
}
```

