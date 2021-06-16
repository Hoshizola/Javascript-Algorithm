# leetcode206：反转链表

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

#### 方法一：迭代

1、判断链表头是否存在或者链表是否只有一个节点，如果是，直接返回`head`；

2、创建一个空节点`prev`作为反转后链表的头节点，记遍历到的当前节点为`cur`，就先用`next`保存`cur`的下一个节点，然后将`cur`的下一个节点指向`prev`，再把`prev`指向该节点，更新`cur`节点为`next`，直到`cur`为空，遍历完毕，返回`prev`。

```javascript
var reverseList = function(head) {
  if(!head || head.next === null) {
    return head
  }
  let prev = null, cur = head
  while(cur) {
    let next = cur.next
    cur.next = prev
    prev = cur
    cur = next
  }
  return prev
}
```

#### 方法二：递归

1、判断链表头是否存在或者链表是否只有一个节点，如果是，直接返回`head`；

2、递归调用链表反转的方法，将原来的指针指向反方向；

```javascript
var reverseList = function(head) {
  if(!head || head.next === null) {
    return head
  }
  // 将链表的最后一个节点作为头节点返回
  let newHead = reverseList(head.next)
  // 反转指针指向
  head.next.next = head
  // 避免形成循环链表
  head.next = null
  return newHead
}
```

