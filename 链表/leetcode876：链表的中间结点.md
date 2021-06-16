# leetcode876：链表的中间结点

定一个头结点为 `head` 的非空单链表，返回链表的中间结点。如果有两个中间结点，则返回第二个中间结点。

**示例 1：**

输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个` ListNode `类型的对象 `ans`，这样：
`ans.val = 3, ans.next.val = 4, ans.next.next.val = 5`, 以及` ans.next.next.next = NULL`.

**示例 2：**

输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。

#### 方法一：两次遍历

1、第一次遍历链表，记录链表的长度`length`；

2、第二次遍历链表，找到下标为`[length/2]`的结点，返回该结点。

```javascript
var middleNode = function(head) {
  let cur = head
  let length = 0
  while(cur) {
    length++
    cur = cur.next
  }
  cur = head
  let index = 0
  while(index < Math.floor(length/2)) {
    cur = cur.next
    index++
  }
  return cur
}
```



#### 方法二：快慢指针

定义一个慢指针和一个快指针，一开始都指向头结点，慢指针每次移动一步，快指针每次移动两次，当快指针到达链表尾部，慢指针所指的结点就是中间结点

```javascript
var middleNode = function(head) {
  let slow = head, fast = head
  while(fast && fast.next) {
    slow = slow.next
    fast = fast.next.next
  }
  return slow
}
```



