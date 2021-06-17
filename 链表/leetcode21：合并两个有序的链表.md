# leetcode21：合并两个有序的链表

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

#### 方法一

1、判断两个链表是否为空，如果其中一个为空，返回另一个链表头结点；都为空返回`null`；

2、创建一个结点`res`充当新的升序链表的首结点，比较两个链表的结点，较小的结点先加入新的链表

3、最后返回`res.next`

```javascript
var mergeTwoLists = function(l1, l2) {
  if(!l1 || !l2) {
    return l1 === null ? l2 : l1
  }
  let res = new ListNode()
  let prev = res
  while(l1 && l2) {
    if(l1.val <= l2.val) {
      prev.next = l1
      prev = l1
      l1 = l1.next
    }else {
      prev.next = l2
      prev = l2
      l2 = l2.next
    }
  }
  if(l1) {
    prev.next = l1
    l1 = l1.next
  }
  if(l2) {
    prev.next = l2
    l2 = l2.next
  }
  return res.next
}
```

#### 方法二：递归

1、判断两个链表是否为空，如果其中一个为空，返回另一个链表头结点；

2、判断链表1的头结点`l1`是否小于等于链表2的头结点`l2`，如果是，说明结点`l1`是所有结点中最小的，递归调用`mergeTwoLists(l1.next, l2)`，且结果返回`l1`，否则调用`mergeTwoLists(l1, l2.next)`，结果返回`l2`。

```javascript
var mergeTwoLists = function(l1, l2) {
  if(!l1 || !l2) {
    return l1 === null ? l2 : l1
  }
  if(l1.val <= l2.val) {
    l1.next = mergeTwoLists(l1.next, l2)
    return l1
  }else {
    l2.next = mergeTwoLists(l1, l2.next)
    return l2
  }
}
```

