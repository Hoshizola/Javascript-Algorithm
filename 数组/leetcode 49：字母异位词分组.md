给你一个字符串数组，请你将 字母异位词 组合在一起。可以按任意顺序返回结果列表。

**示例 1:**

**输入:** `strs` =` ["eat", "tea", "tan", "ate", "nat", "bat"]`

**输出:** `[["bat"],["nat","tan"],["ate","eat","tea"]]`

**解释：**

- 在 `strs` 中没有字符串可以通过重新排列来形成 `"bat"`。
- 字符串 `"nat"` 和 `"tan"` 是字母异位词，因为它们可以重新排列以形成彼此。
- 字符串 `"ate"` ，`"eat"` 和 `"tea"` 是字母异位词，因为它们可以重新排列以形成彼此。

**示例 2:**

**输入:** `strs =[""]`

**输出:**` [[""]]`

**示例 3:**

**输入:** `strs = ["a"]`

**输出:** `[["a"]]`

**思路**：
由于互为字母异位词的两个字符串包含的字母相同，因此对两个字符串分别进行排序之后得到的字符串一定是相同的，故可以将排序之后的字符串作为哈希表的键。
```js
var groupAnagrams = function(strs) {
    const map = new Map()
    for(let item of strs) {
        let model = [...item].sort().join('')
        if (map.has(model)) {
            map.get(model).push(item)
        } else {
            map.set(model, [item])
        }
    }
    return [...map.values()]
};
```
