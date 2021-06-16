# leetcode141：环形链表

给定一个链表，判断链表中是否有环。如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，我们使用整数` pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos `是 -1，则在该链表中没有环。注意：`pos` 不作为参数进行传递，仅仅是为了标识链表的实际情况。如果链表中存在环，则返回` true` 。 否则，返回 `false` 。

#### 方法一：标记法

1、若链表头指针不存在或者链表只有一个节点，肯定不是环形链表；

2、遍历链表，给每个节点加上`flag`属性，并给已经遍历的节点设置为`flag`，如果遍历到一个节点`flag`已经为`true`，说明存在环，返回`true`。

```javascript
var hasCycle = function(head) {
  while(head){
      if(head.flag){
          return true
      }
      head.flag = true
      head = head.next
  }
  return false
};
```

#### 方法二：快慢指针

1、若链表头指针不存在或者链表只有一个节点，肯定不是环形链表；

2、定义两个指针，快指针一次走两步，慢指针一次走一步，若快慢指针能够相遇，说明是环形链表，因为快指针总是比慢指针多走一步，如果有环，快指针总会追上慢指针。

```javascript
var hasCycle2 = function(head) {
  if(!head || head.next === null) {
    return false
  }
  let slow = head, fast = head.next.next
  while(fast && fast.next) {
    if(slow === fast) {
      return true
    }
    slow = slow.next
    fast = fast.next.next
  }
  return false
}
```

