# leetcode112：路径总和

给你二叉树的根节点 root 和一个表示目标和的整数 targetSum，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和 targetSum 。

#### 方法一：深度优先搜索

用递归的思想，搜索从当前节点的子节点到叶子节点是否存在和为`sum-val`的路径，当到达叶子节点时，直接判断节点`val`是否等于目标`sum`

```javascript
var hasPathSum = function(root, targetSum) {
  if(!root) {
    return false
  }
  if(!root.left && !root.right && root.val === targetSum) {
    return true
  }
  return hasPathSum(root.left, targetSum - root.val) || hasPathSum(root.right, targetSum - root.val)
}
```

#### 方法二：广度优先搜索

- 用一个队列存放遍历到的节点，同时用另一个队列存放从根节点到该节点的路径和，两个队列一一对应
- 在将节点的子节点入队列时，先判断是否为叶子节点，如果是，则根节点到该节点的路径和是否为目标和，是则返回`true`

```javascript
var hasPathSum = function(root, targetSum) {
  if(!root) {
    return 0
  }
  if(!root.left && !root.right) {
    return root.val === targetSum
  }
  let nodeArr = []
  let sumArr = []
  nodeArr.push(root)
  sumArr.push(root.val)
  while(nodeArr.length > 0) {
    let size = nodeArr.length
    while(size > 0) {
      let popNode = nodeArr.shift()
      let popSum = sumArr.shift()
      if(popNode.left) {
        if(!popNode.left.left && !popNode.left.right && popSum + popNode.left.val === targetSum) {
          return true
        }
        nodeArr.push(popNode.left)
        sumArr.push(popSum + popNode.left.val)
      }
      if(popNode.right) {
        if(!popNode.right.left && !popNode.right.right && popSum + popNode.right.val === targetSum) {
          return true
        }
        nodeArr.push(popNode.right)
        sumArr.push(popSum + popNode.right.val)
      }
      size--
    }
  }
  return false
}
```



