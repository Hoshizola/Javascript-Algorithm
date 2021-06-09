# leetcode104：二叉树的最大深度

给定一个二叉树，找出其最大深度。二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

##### 方法一：深度优先搜索

要求二叉树的最大深度，就需要求左子树和右子树的最大深度。同理，要求左(右)子树的最大深度，就需要求左(右)子树的左右子树的最大深度，直到叶节点。用递归求解。

```javascript
var maxDepth = function(root) {
  if(root === null) {
    return 0
  }
  let leftDepth = maxDepth(root.left)
  let rightDepth = maxDepth(root.right)
  return 1 + Math.max(leftDepth, rightDepth)
};
```

##### 方法二：广度优先搜索

1、创建一个数组充当队列，如果根节点不为空，先把根节点加入到队列中，并初始化层数`res=0`；

2、记录队列中的节点个数，这个节点个数就是队首节点所在层中的节点个数。把该层中所有节点都出队列后，层数`res+1`，同时把出队列节点的左右节点加入队列；

3、重复以上操作，直到队列为空，res的值就是树的最大深度。

```javascript
var maxDepth = function(root) {
  if(root === null) {
      return 0
  }
  let queue = new Array()
  queue.push(root)
  let res = 0
  // 队列中还有节点
  while(queue.length > 0) {
    // 记录当前所在层数中的节点个数
    let len = queue.length
    // 取出该层中全部的节点
    while(len > 0) {
      // 队首节点出队列
      let node = queue.shift()
      if(node.left) {
        queue.push(node.left)
      }
      if(node.right) {
        queue.push(node.right)
      }
      len--
    }
    res++
  }
  return res
};
```



