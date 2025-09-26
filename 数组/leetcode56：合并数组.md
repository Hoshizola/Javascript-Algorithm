以数组 `intervals` 表示若干个区间的集合，其中单个区间为 `intervals[i] = [starti, endi]` 。请你合并所有重叠的区间，并返回 _一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间_ 。

**示例 1：**

**输入：** intervals = `[[1,3],[2,6],[8,10],[15,18]]`
**输出：** ` [[1,6],[8,10],[15,18]]`
**解释：** 区间` [1,3] `和 `[2,6]` 重叠, 将它们合并为` [1,6]`.

**示例 2：**

**输入：** intervals =` [[1,4],[4,5]]`
**输出：** `[[1,5]]`
**解释：** 区间` [1,4] `和` [4,5]` 可被视为重叠区间。

**示例 3：**

**输入：** intervals =` [[4,7],[1,4]]`
**输出：** `[[1,7]]`
**解释：** 区间` [1,4]` 和` [4,7]` 可被视为重叠区间。

**提示：**

- `1 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 104`

##### 思路
如果我们按照区间的左端点排序，那么在排完序的列表中，可以合并的区间一定是连续的。如下图所示，标记为蓝色、黄色和绿色的区间分别可以合并成一个大区间，它们在排完序的列表中是连续的：
![[Pasted image 20250926192818.png]]
我们用数组 merged 存储最终的答案。

首先，我们将列表中的区间按照左端点升序排序。然后我们将第一个区间加入 merged 数组中，并按顺序依次考虑之后的每个区间：

如果当前区间的左端点在数组 merged 中最后一个区间的右端点之后，那么它们不会重合，我们可以直接将这个区间加入数组 merged 的末尾；

否则，它们重合，我们需要用当前区间的右端点更新数组 merged 中最后一个区间的右端点，将其置为二者的较大值。

##### 代码
```javascript
var merge = function(intervals) {
    intervals.sort((a, b) => a[0] - b[0])
    let prev = intervals[0]
    let result = []
    for (let i = 1; i < intervals.length; i++) {
        const cur = intervals[i]
        if (prev[1] >= cur[0]) {
            prev[1] = Math.max(prev[1], cur[1])
        } else {
            result.push(prev)
            prev = cur
        }
   }
   result.push(prev)
   return result
}
```
