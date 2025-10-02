[148. 排序链表 - 力扣（LeetCode）](https://leetcode.cn/problems/sort-list/description/?envType=study-plan-v2&envId=top-100-liked)

给你链表的头结点 `head` ，请将其按 **升序** 排列并返回 **排序后的链表** 。

##### 代码

采用归并排序的思想

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var sortList = function(head) {
    if (!head || !head.next) return head
    let slow = head, fast = head, preSlow = null
    while(fast && fast.next) {
        preSlow = slow
        slow = slow.next
        fast = fast.next.next
    }
    preSlow.next = null
    const left = sortList(head)
    const right = sortList(slow)
    const newHead = mergeSort(left, right)
    return newHead
}

function mergeSort(leftHead, rightHead) {
    let head = new ListNode(0), currentNode = head
    while(leftHead && rightHead) {
        if (leftHead.val < rightHead.val) {
            currentNode.next = leftHead
            leftHead = leftHead.next
        } else {
            currentNode.next = rightHead
            rightHead = rightHead.next
        }
        currentNode = currentNode.next
    }
    if(leftHead) {
        currentNode.next = leftHead
    }
    if(rightHead) {
        currentNode.next = rightHead
    }
    return head.next
}
```
