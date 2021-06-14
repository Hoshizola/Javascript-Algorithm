# leetcode235：二叉搜索树的最近公共祖先

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

#### 方法一：递归

- 比较根节点和`p`、`q`的值，若都小于根节点，则往左子树深度遍历；若都大于根节点，则往右子树深度遍历；
- 当`p`和`q`两个节点不在父节点的同一边时，即出现了分岔点，该节点就是要找的最近公共祖先。

```javascript
var lowestCommonAncestor = function(root, p, q) {
  if(!root) {
    return null
  }
  if(root.val < p.val && root.val < q.val) {
    lowestCommonAncestor(root.right, p, q)
  }
  if(root.val > p.val && root.val > q.val) {
    lowestCommonAncestor(root.left, p, q)
  }
  return root
}
```

#### 方法二：迭代

思路与递归的方法一样，一般来说能用递归的地方就能用迭代。

```javascript
var lowestCommonAncestor = function(root, p, q) {
  while(root) {
    if(root.val < p.val && root.val < q.val) {
      root = root.right
    }
    if(root.val > p.val && root.val > q.val) {
      root = root.left
    }
    if((root.val >= p.val && root.val <= q.val) || (root.val <= p.val && root.val >= q.val)) {
      return root
    }
  }
}
```

#### 方法三：路径比较

- 用深度遍历分别用数组记录从根节点到`p`节点的路径和从根节点到`q`节点的路径
- 比较两个数组，找到节点值相同的最大索引值

```javascript
var lowestCommonAncestor = function(root, p, q) {
  let pPath = [], qPath = []
  // 备份根节点，因为在遍历的过程中，根节点会转移
  let root_copy = root
  // 求到p节点的路径
  while(root_copy !== p) {
    pPath.push(root_copy)
    if(p.val < root_copy.val) {
      root_copy = root_copy.left
    }else {
      root_copy = root_copy.right
    }
  }
  pPath.push(root_copy)
  root_copy = root
  // 求到q节点的路径
  while(root_copy !== q) {
    qPath.push(root_copy)
    if(q.val < root_copy.val) {
      root_copy = root_copy.left
    }else {
      root_copy = root_copy.right
    }
  }
  qPath.push(root_copy)
  let index = 0
  while(index < pPath.length && index < qPath.length) {
    if(pPath[index].val === qPath[index].val) {
      index++
    }
  }
  return pPath[index] 
}
```

