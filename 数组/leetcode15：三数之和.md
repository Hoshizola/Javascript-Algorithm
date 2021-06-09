# leetcode15：三数之和

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。注意：答案中不可以包含重复的三元组。

示例 1：

输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]

示例 2：

输入：nums = []
输出：[]

示例 3：

输入：nums = [0]
输出：[]

### 思路

解决方式排序+双指针。

1、先将数组按从小到大排好序，然后进行第一重循环。若当前遍历的值大于0，则终止循环，因为后面的值都会比当前值大，不存在三数之和为`0`的结果。若遍历到值与上一次的一样，跳过。

2、将指针分别指向当前遍历对象的下一个对象和最后一个对象。

3、如果当前遍历的值与俩指针的值之和小于`0`，左指针右移，若右移后的数字和之前的一样，继续后移；如果大于`0`，右指针左移，若左移后的数字和之前的一样，继续左移。若等于`0`，记录下答案。右指针继续左移，左指针继续右移，知道左指针不再小于右指针，开始下一次循环。

```javascript
var threeSum = function(nums) {
  let res = []
  let len = nums.length
  let second, last, sum
  nums.sort((a,b) => a - b)
  for(let i = 0; i < len - 2; i++) {
    if(nums[i] > 0) break
    if(nums[i] === nums[i-1]) continue
    second = i + 1
    last = len - 1
    while(second < last) {
      sum = nums[i] + nums[second] + nums[last]
      if(sum < 0) {
        second++
      }else if(sum > 0) {
        last--
      }else{
        res.push([nums[i], nums[second], nums[last]])
        while(second < last && nums[second] === nums[second+1]){
          second++
        }
        second++
        while(second < last && nums[last] === nums[last-1]) {
          last--
        } 
        last--
      }
    }
  }
  return res
}
```

