# leetcode160：相交链表

给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 `null` 。

#### 方法一：标记法

1、先遍历第一个链表，每遍历一个结点，就标记为`true`；

2、再遍历第二个链表，若遍历到一个结点已经为`true`，返回该结点；若没有结点为`true`，说明两个链表不相交，返回`null`。

```javascript
var getIntersectionNode = function(headA, headB) {
  let a = headA, b = headB
  while(a) {
    a.flag = true
    a = a.next
  }
  while(b) {
    if(b.flag) {
      return b
    }
    b = b.next
  }
  return null
};
```

#### 方法二：双指针

1、分别用指针指向两个链表的头结点，依次往后遍历；

2、若链表`A`走到结点为空，则将指针指向链表`B`头结点；若链表`B`走到结点为空，则将指针指向链表`A`头结点；

3、两个指针第一次相遇时，该结点就是相交结点。

```javascript
var getIntersectionNode = function(headA, headB) {
  if(!headA || !headB) {
    return null
  }
  if(headA === headB) {
    return headB
  }
  let a = headA, b = headB
  while(a && b) {
    a = a.next
    b = b.next
  }
  if(!a) {
    a = headB
  }
  if(!b) {
    b = headA
  }
  while(a && b) {
    a = a.next
    b = b.next
  }
  if(!a) {
    a = headB
  }
  if(!b) {
    b = headA
  }
  while(a && b) {
    if(a === b) {
      return a
    }
    a = a.next
    b = b.next
  }
  return null
}
```

