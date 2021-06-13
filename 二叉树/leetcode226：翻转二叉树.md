# leetcode226：翻转二叉树

翻转一棵二叉树。

**示例：**

输入：

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

输出：

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

#### 方法：递归

总体思路是用递归的方法，先翻转左子树，再翻转右子树，然后交换左右子树的位置

```javascript
var invertTree = function(root) {
  if(!root) {
    return null
  } 
  if(!root.left && !root.right) {
    return root
  }
  let invertLeft = invertTree(root.left)
  let invertRight = invertTree(root.right)
  root.left = invertRight
  root.right = invertLeft
  return root
}
```

