给定一个二叉搜索树的根节点 `root` ，和一个整数 `k` ，请你设计一个算法查找其中第 `k` 小的元素（从 1 开始计数）。

**思路和算法**

因为二叉搜索树和中序遍历的性质，所以二叉搜索树的中序遍历是按照键增加的顺序进行的。于是，我们可以通过中序遍历找到第 k 个最小元素。

**代码**
```javascript
var kthSmallest = function(root, k) {
    const stack = []
    while(root != null || stack.length) {
        while(root != null) {
            stack.push(root)
            root = root.left
        }
        root = stack.pop()
        --k
        if (k === 0) {
            break
        }
        root = root.right
    }
    return root.val
}
```
