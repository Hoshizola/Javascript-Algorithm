# leetcode234：回文链表

请判断一个链表是否为回文链表。

**示例 1:**

```
输入: 1->2
输出: false
```

**示例 2:**

```
输入: 1->2->2->1
输出: true
```

#### 方法一

先将链表结点的值放进数组，然后将数组转化后的字符串和反转后的数组转化后的字符串进行比较

```javascript
var isPalindrome = function(head) {
  if(!head || !head.next) {
    return true
  }
  let arr = [], cur = head
  while(cur) {
    arr.push(cur.val)
    cur = cur.next
  }
  return arr.join('') === arr.reverse().join('')
}
```

#### 方法二

将链表结点放进数组，用双指针遍历数组，从最左端和最右端开始遍历

```javascript
var isPalindrome = function(head) {
  if(!head || !head.next) {
    return true
  }
  let arr = [], cur = head
  while(cur) {
    arr.push(cur.val)
    cur = cur.next
  }
  let left = 0, right = arr.length - 1
  while(left <= right) {
    if(arr[left] !== arr[right]) {
      return false
    }
    left++
    right--
  }
  return true
}
```

