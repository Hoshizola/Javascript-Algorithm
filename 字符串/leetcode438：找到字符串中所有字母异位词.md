
给定两个字符串 `s` 和 `p`，找到 `s` 中所有 `p` 的 **异位词** 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

**示例 1:**

**输入:** s = "cbaebabacd", p = "abc"
**输出:** `[0,6]`
**解释:**
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。

 **示例 2:**

**输入:** s = "abab", p = "ab"
**输出:**  `[0,1,2]`
**解释:**
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。

**提示:**

- `1 <= s.length, p.length <= 3 * 104`
- `s` 和 `p` 仅包含小写字母

###### 代码一
简易版（超时）
```javascript
var findAnagrams = function(s, p) {
    const length = p.length
    const pSort = [...p].sort().join('')
    const s_length = s.length
    const result = []

    for(let i = 0; i <= s_length - length; i++) {
        const sub = s.slice(i, i+length)
        const subSort = [...sub].sort().join('')
        if (subSort === pSort) {
            result.push(i)
        }
    }
    return result
}
console.log(findAnagrams('abab', 'ab'))
```

##### 代码二
#滑动窗口 #哈希表

核心思想：
1. 用一个哈希表 `map` 来记录字符串 `p` 中每个字符的出现次数。
2. 在字符串 `s` 上维护一个长度为 `p.length` 的滑动窗口。
3. 用同一个哈希表 `map` 来动态地记录当前窗口内每个字符的出现次数与 `p` 的差异。
4. 如果在某个时刻，哈希表 `map` 中所有字符的计数都为 0，说明当前窗口与 `p` 是异位词。

```javascript
var findAnagrams = function(s, p) {
  if (p.length > s.length) return []
  const map = new Map(), res = []
  for (let item of p) {
    map.set(item, (map.get(item) || 0) + 1)
  }
  // 初始化滑动窗口
  let r = 0
  for (; r < p.length; r++) {
    if (map.has(s[r])) {
      map.set(s[r], map.get(s[r]) - 1)
    }
  }
  for (let l = 0; r <= s.length; r++, l++) {
    if ([...map.values()].every(v => v === 0)) {
      res.push(l)
    }
    // 移动左边界还原
    if (map.has(s[l])) {
      map.set(s[l], map.get(s[l]) + 1)
    }
    // 移动右边界，再次抵消
    if (map.has(s[r])) {
      map.set(s[r], map.get(s[r]) - 1)
    }
  }
  return res
};
```
