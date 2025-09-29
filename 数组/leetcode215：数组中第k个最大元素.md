给定整数数组 `nums` 和整数 `k`，请返回数组中第 **k**个最大的元素。

请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。

你必须设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

**示例 1:**

**输入:** `[3,2,1,5,6,4],` k = 2
**输出:** 5

**示例 2:**

**输入:** `[3,2,3,1,2,4,5,5,6],` k = 4
**输出:** 4

**提示：**

- `1 <= k <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

##### 方法一：
```javascript
var findKthLargest = function(nums, k) {
    if (nums.length === 0) {
        return undefined
    }
    if (nums.length === 1) {
        return k === 1 ? nums[0] : undefined
    }
    nums.sort((a,b) => b - a)
    return nums[k-1]
}
```

##### 方法二：快速排序
```javascript
/**
 * 主函数：查找数组中第 k 大的元素
 * @param {number[]} nums - 输入的数组
 * @param {number} k - 目标是第 k 大元素（注意：第1大是最大的）
 * @return {number}
 */

var findKthLargest = function(nums, k) {
  const n = nums.length;
  // 题目要求第 k 大，其实是“第 n-k 小”（因为下标从0开始）
  // 例如：找第2大，其实是第 n-2 小
  return quickselect(nums, 0, n - 1, n - k);
};
/**
 * 快速选择核心函数
 * @param {number[]} nums - 数组
 * @param {number} l - 左边界
 * @param {number} r - 右边界
 * @param {number} k - 目标索引（从0开始）即“第 k 小的元素”索引
 * @return {number} - 返回该元素值
 */
function quickselect(nums, l, r, k) {
  // 递归终止条件：当只剩一个元素时
  if (l === r) return nums[k];
  // 选择一个枢轴（pivot），这里选的是第一个元素
  const x = nums[l];
  let i = l - 1, j = r + 1;
  // 快排式分区，调整数组，使得：
  // 所有 < pivot 的元素在左边
  // 所有 > pivot 的元素在右边
  // 注意这里是“荷兰国旗划分法”的经典做法
  while (i < j) {
    // 从左往右找：找到第一个 ≥ pivot 的元素
    do i++; while (nums[i] < x);
    // 从右往左找：找到第一个 ≤ pivot 的元素
    do j--; while (nums[j] > x);
    // 如果 i 和 j 没有交叉，就交换它们
    if (i < j) {
      [nums[i], nums[j]] = [nums[j], nums[i]];
    }
  }
  // 此时 j 是分区点：左边都是 <= x，右边是 >= x
  // 根据 k 与 j 的关系，决定往哪一边递归
  if (k <= j) {
    // 第 k 小在左半部分
    return quickselect(nums, l, j, k);
  } else {
    // 第 k 小在右半部分
    return quickselect(nums, j + 1, r, k);
  }
}
```

