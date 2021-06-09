# leetcode100：相同的树

给你两棵二叉树的根节点` p `和 `q `，编写一个函数来检验这两棵树是否相同。如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

**示例 1：**

输入：p = [1,2,3], q = [1,2,3]
输出：true

**示例 2：**

输入：p = [1,2], q = [1,null,2]
输出：false

**示例 3：**

输入：p = [1,2,1], q = [1,1,2]
输出：false
链接：https://leetcode-cn.com/problems/same-tree

##### 方法一：深度优先搜索

1、如果给出的两个根节点都为`null`，则结果为`true`；

2、如果给出的两个根节点其中有一个为`null`，则结果为`false`；

3、如果根节点都不为`null`但值不同，则结果为`false`；

4、如果根节点都不为`null`且值相同，递归比较`p`的左子树和`q`的左子树、`p`的右子树和`q`的右子树，若结果都为`true`，说明两棵树完全相同。

```javascript
var isSameTree = function(p, q) {
  if(p === null || q === null) {
    return true
  }else if(p === null || q === null) {
    return false
  }else if(p.val !== q.val) {
    return false
  }
  return isSameTree(p.left, q.left) && isSameTree(p.right, q.right)
}
```

##### 方法二：广度优先搜索

1、首先比较根节点，方法与深度优先搜索一样；

2、分别用两个队列存放`p`树节点和`q`树节点。先判断p树根节点的左子节点是否存在，若存在，给节点对象增加`flag`属性表示该节点的左子节点属性，给p树根节点的右子节点和q树根节点的左右子节点进行同样的操作；

3、此时队列中存放的是同一层的节点元素，比较两个队列中的元素个数是否相同，若不同，说明同一层的节点数不同，直接返回`false`；若相同，逐次取出队首，比较两个节点的左右节点属性和值，其中一个不同返回`false`；

4、各自取出队首并且比较结果一致后，在队列中又加入各自的左右子节点；

5、重复进行步骤3和4，直到有空队列为止；

6、若队列不都为空，说明两棵树的节点个数不一样，返回`false`，否则返回`true`；

```javascript
var isSameTree = function(p, q) {
  if(p === null && q === null) {
     return true
  }else if(p === null || q === null) {
    return false
  }else if(p.val !== q.val) {
    return false
  }
  // 存放p树节点的队列
  let pQueue = new Array()
  // 存放q树节点的队列
  let qQueue = new Array()
  if(p.left) {
    p.left.flag = 'left'
    pQueue.push(p.left)
  }
  if(p.right) {
    p.right.flag = 'right'
    pQueue.push(p.right)
  }
  if(q.left) {
    q.left.flag = 'left'
    qQueue.push(q.left)
  }
  if(q.right) {
    q.right.flag = 'right'
    qQueue.push(q.right)
  }
  while(pQueue.length > 0 && qQueue.length > 0) {
    let pLen = pQueue.length
    let qLen = qQueue.length
    // 比较节点的左右节点属性和值是否相同
    if(pLen !== qLen) {
      return false
    }
    while(pLen > 0) {
      let pNode = pQueue.shift()
      let qNode = qQueue.shift()
      if(pNode.flag !== qNode.flag || pNode.val !== qNode.val) {
        return false
      }
      if(pNode.left) {
        pNode.left.flag = 'left'
        pQueue.push(pNode.left)
      }
      if(pNode.right) {
        pNode.right.flag = 'right'
        pQueue.push(pNode.right)
      }
      if(qNode.left) {
        qNode.left.flag = 'left'
        qQueue.push(qNode.left)
      }
      if(qNode.right) {
        qNode.right.flag = 'right'
        qQueue.push(qNode.right)
      }
      pLen--
    }
  }
  // 退出循环后，检查两个队列长度是否相等
  if(pQueue.length !== qQueue.length) {
    return false
  }
  return true
}
```



