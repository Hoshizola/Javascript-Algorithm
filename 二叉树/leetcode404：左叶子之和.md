# leetcode404：左叶子之和

计算给定二叉树的所有左叶子之和。

**示例：**

```
    3
   / \
  9  20
    /  \
   15   7
```

在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24。

#### 方法一：深度优先遍历

定义一个方法，用于在递归搜索树时累加左叶子节点之和

```javascript
var sumOfLeftLeaves = function(root) {
  let sum = 0
  let getSum = function(root) {
    if(!root || (!root.left && !root.right)) {
      return
    }
    // 判断左叶子节点
    if(root.left && !root.left.left && !root.left.right) {
      sum += root.left.val
    }
    getSum(root.left)
    getSum(root.right)
  }
  getSum(root)
  return sum
}
```

#### 方法二：广度优先遍历

对二叉树进行广度优先遍历，当遍历到左叶子节点，累加和

```javascript
var sumOfLeftLeaves = function(root) {
  let sum = 0
  if(!root || (!root.left && !root.right)) {
    return sum
  }
  let nodeArr = []
  nodeArr.push(root)
  while(nodeArr.length) {
    let size = nodeArr.length
    while(size > 0) {
      let popNode = nodeArr.pop()
      if(popNode.left && !popNode.left.left && !popNode.left.right) {
        sum += popNode.left.val
      }
      if(popNode.left) {
        nodeArr.push(popNode.left)
      }
      if(popNode.right){
        nodeArr.push(popNode.right)
      }
      size--
    }
  }
  return sum
}
```

