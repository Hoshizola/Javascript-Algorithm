# leetcode111：二叉树的最小深度

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

#### 方法一：深度优先搜索

要求得二叉树的最小深度，就需要求得左右子树的最小深度，此时需要注意，在深度遍历的过程中若其中一个子节点不存在，则最小深度取决于另一棵子树。如果根节点不存在，返回`0`，若子节点都不存在，则返回`1`。

```javascript
var minDepth = function(root) {
  if(!root) {
    return 0
  }
  if(!root.left && !root.right) {
    return 1
  }
  if(!root.right) {
    return minDepth(root.left) + 1
  }
  if(!root.left) {
    return minDepth(root.right) + 1
  }
  return Math.min(minDepth(root.left), minDepth(root.right)) + 1
}
```

#### 方法二：广度优先搜索

用一个数组存放广度优先搜索到的节点，只要还没找到叶节点，遍历完一层节点后，层数要`+1`，当找到一个叶节点，结束算法，返回结果。

```javascript
var minDepth = function(root) {
  if(!root) {
    return 0
  }
  // 存放节点的数组
  let nodeArr = []
  // 记录结果层数
  let result = 0
  // 标记是否要继续广度优先搜索，若为false则搜索结束
  let flag = true
  nodeArr.push(root)
  while(nodeArr.length > 0 && flag) {
    let size = nodeArr.length
    // 遍历同一层的节点，若找到一个叶节点，就结束循环，返回结果
    while(size > 0) {
      let popNode = nodeArr.shift()
      if(!popNode.left && !popNode.right) {
        flag = false
        break
      }else {
        if(popNode.left) {
          nodeArr.push(popNode.left)
        } 
        if(popNode.right) {
          nodeArr.push(popNode.right)
        }
      }
      size--
    }
    result++
  }
  return result
}
```

