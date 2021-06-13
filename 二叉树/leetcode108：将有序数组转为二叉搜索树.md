# leetcode108：将有序数组转为二叉搜索树

给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。

高度平衡 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。

#### 方法

- 数组是一个有序数组，且树是一颗二叉搜索树，因此数组的中心节点为该树的根节点。
- 确定根节点后，需要确定左子树和右子树，左子树由左半部分的数组构成，右子树由右半部分的数组构成，因此构建树的过程是一个递归的过程。
- 定义一个函数，用来将数组中的一部分构建成一颗二叉搜索树。
- 当数组中只有一个元素时，其左右节点为`null`，且作为该数组的根节点返回。

```javascript
function TreeNode(val, left, right) {
    this.val = (val===undefined ? 0 : val)
    this.left = (left===undefined ? null : left)
    this.right = (right===undefined ? null : right)
}

var sortedArrayToBST = function(nums) {
  return buildTree(nums, 0, nums.length - 1)
}
function buildTree(list, left, right) {
  if(left > right) {
    return null
  }
  let mid = Math.floor((left + right) / 2)
  let newNode = new TreeNode(list[mid])
  newNode.left = buildTree(list, left, mid - 1)
  newNode.right = buildTree(list, mid + 1, right)
  return newNode
}
```

