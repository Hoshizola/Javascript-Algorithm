# leetcode189：旋转数组

给定一个数组，将数组中的元素向右移动 `k` 个位置，其中 `k` 是非负数。

### 思路

数组中的元素向右移动一个元素，相当于将最后一个元素删除，并把它放在数组的第一个，移动`k`次就进行`k`次上述操作。如果`k`是数组长度的倍数，相当于没有移动，所以实际移动的次数是`k%length`。

##### 方法一

利用数组的`pop()`删除并返回最后一个元素，用`unshift()`将元素插入到数组头部

```javascript
var rotate = function(nums, k) {
  let len = nums.length 
  let count = k % len
  if(count === 0) {
    return nums
  }
  for(let i = 0; i < count; i++) {
    nums.unshift(nums.pop())
  }
  return nums
};
```

##### 方法二

用`splice()`方法先截取数组的后`k`个元素，再把这`k`个元素用`unshift()`整体插入到数组前面

```javascript
var rotate = function(nums, k) {
  let len = nums.length
  let count = k % len
  nums.unshift(...nums.splice(len - count, count))
  return nums
};
```

