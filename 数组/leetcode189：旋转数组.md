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

##### 方法三（leetcode能通过）

1. 首先对整个数组实行翻转，这样子原数组中需要翻转的子数组，就会跑到数组最前面。
2. 这时候，从 k 处分隔数组，左右两数组，各自进行翻转即可。
```javascript
let reverse = function(nums, start, end){
    while(start < end){
        [nums[start++], nums[end--]] = [nums[end], nums[start]];
    }
}

let rotate = function(nums, k) {
    k %= nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
    return nums;
};
```

