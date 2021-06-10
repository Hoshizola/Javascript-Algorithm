# leetcode101(剑指offer28)：对称二叉树

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的，但是 [1,2,2,null,3,null,3] 则不是镜像对称的。

#### 方法一：递归

1、判断根节点是否为空，如果为空，返回`true`，如果不为空，判断其左子树和右子树是否对称；

2、要判断左子树和右子树是否对称，需要先判断左子节点和右子节点是否相等，若其中有一个为空，返回`false`，若都不为空但是值不相等，也返回`false`，若都为空或者都不为空且值相等，返回`true`；

3、递归判断左子节点的左子树和右子节点的右子树、左子节点的右子树和右子节点的左子树是否对称。

```javascript
var isSymmetric = function(root) {
  if(root === null) {
    return true
  }
  function isTwo(left, right) {
    if(left === null && right === null) {
      return true
    }else if(left === null || right === null) {
      return false
    }else if(left.val !== right.val) {
      return false
    }
    return isTwo(left.left, right.right) && isTwo(left.right, right.left)
  }

  return isTwo(root.left, root.right)
};
```

#### 方法二：迭代

此迭代方法可以看成广度优先搜索。

1、用`queue`队列保存同一层级的节点对象，每一次都从队首取出节点，并保存在`levelNodes`队列中

2、遍历过程中把每个节点的左右子节点存进`queue`队列。

3、之后遍历`levelNodes`，比较`levelNodes[i]`和`levelNodes[length - 1 - i]`是否相等。

4、重复以上过程，直到`queue`队列为空。

```javascript
var isSymmetric = function(root) {
  if(!root) {
    return true
  }
  let queue = [root.left, root.right]
  while(queue.length) {
    let len = queue.length
    let levelNodes = []
    while(len) {
      let node = queue.shift()
      levelNodes.push(node)
      if(node) {
        queue.push(node.left)
        queue.push(node.right)
      }
      len--
    }
    for(let i = 0, l = levelNodes.length; i > l; i++) {
      if(levelNodes[i] !== null 
        && levelNodes[l - 1 - i] !== null 
        && levelNodes[i].val !== levelNodes[l - 1 - i].val){
        return false
      }
      if((levelNodes[i] === null && levelNodes[l - 1 - i] !== null) 
         || (levelNodes[i] !== null && levelNodes[l - 1 - i] === null)) {
        return false
      }
    }
  }
  return true
};
```

