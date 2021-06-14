# leetcode257：二叉树的所有路径

给定一个二叉树，返回所有从根节点到叶子节点的路径。

说明: 叶子节点是指没有子节点的节点。

**示例:**

输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3

#### 方法一：深度优先搜索

深度搜索二叉树，每遍历到一个节点就加入到路径`path`中，并把`path`往左右子树传递，当到达叶子节点时，将`path`添加进数组

```javascript
var binaryTreePaths = function(root) {
  let result = []
  let collectPaths = function(root, path) {
    if(!root) {
      return
    }
    // 到达叶节点
    if(!root.left && !root.right) {
      path += root.val
      result.push(path)
    }else {
      path += root.val + '->'
      collectPaths(root.left, path)
      collectPaths(root.right, path)
    }
  }
  collectPaths(root, '')
  return result
}
```

#### 方法二：广度优先搜索

- 使用两个队列，一个队列存放广度遍历的节点，另一个队列存放从根节点到该节点的路径
- 在向队列中加入节点时，判断该节点是否是叶子节点，如果是就将对应的路径加入结果数组中

```javascript
var binaryTreePaths = function(root) {
  let result = []
  if(!root) {
    return result
  }
  let nodeArr = []
  let nodePaths = []
  nodeArr.push(root)
  nodePaths.push(root.val.toString())
  while(nodeArr.length) {
    let size = nodeArr.length
    while(size > 0) {
      let popNode = nodeArr.pop()
      let popPath = nodePaths.pop()
      if(!popNode.left && !popNode.right) {
        result.push(popPath)
      }
      if(popNode.left) {
        nodeArr.push(popNode.left)
        nodePaths.push(popPath + '->' + popNode.left.val)
      }
      if(popNode.right) {
        nodeArr.push(popNode.right)
        nodePaths.push(popPath + '->' + popNode.right.val)
      }
      size--
    }
  }
  return result
}
```

