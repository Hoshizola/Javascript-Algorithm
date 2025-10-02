#双指针

详细内容：[11. 盛最多水的容器 - 力扣（LeetCode）](https://leetcode.cn/problems/container-with-most-water/description/?envType=study-plan-v2&envId=top-100-liked)

给定一个长度为 `n` 的整数数组 `height` 。有 `n` 条垂线，第 `i` 条线的两个端点是 `(i, 0)` 和 `(i, height[i])` 。

找出其中的两条线，使得它们与 `x` 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

##### 代码

- **时间复杂度 O(N)​ ：** 双指针遍历一次底边宽度 N​​ 。
- **空间复杂度 O(1)​ ：** 变量 i , j , result 使用常数额外空间。

```javascript
const len = height.length
    let result = 0, i = 0, j = len - 1
    while(i < j) {
        let v
        if (height[i] < height[j]) {
            v = (j - i) * height[i]
            result = Math.max(result, v)
            i++
        } else {
            v = (j - i) * height[j]
            result = Math.max(result, v)
            j--
        }
    }
    return result
```

