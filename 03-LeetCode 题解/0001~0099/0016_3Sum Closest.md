# [16. 3Sum Closest](https://leetcode-cn.com/problems/3sum-closest/)
## 题目
Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.

Return <em>the sum of the three integers</em>.

You may assume that each input would have exactly one solution.

 

<strong>Example 1:</strong>

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

<strong>Example 2:</strong>

```
Input: nums = [0,0,0], target = 1
Output: 0
```

 

<strong>Constraints:</strong>


- `3 <= nums.length <= 1000`
- `-1000 <= nums[i] <= 1000`
- `-10^4 <= target <= 10^4`



## 题目大意

在给定整数数组`nums`中找出和最接近`target`的 3 个数，返回它们的和

## 解题思路

本题与 [0015.3Sum](../0001~0099/0015.3Sum.md) 类似，可以用**排序 + 双指针**的方法来解决

1. 排序（从小到大，和从大到小均可，这里我们从小到大排序）

   好处：在确定一个数的前提下，寻找另外两个数的时间复杂度可以从`O(n^2)`优化至`O(n)`，解释如下

2. 顺序遍历数组，对于每一个元素`nums[i]`，我们都要在它后面的元素中找到两个数`nums[j]`、`nums[k]`，使得三个数的和为尽量靠近 target

3. 对于每个确定的`nums[i]`，找到剩余两个数的时间复杂度为`O(n^2)`。又因为数组已经有序，所以剩余两个数如果从两头开始寻找，即下标从`j = i + 1`、`k = nums.length - 1`向中间靠拢遍历。

4. 若当前 3 个数的和小于 target ，说明和不够大，则`j++`，即让第二个数大一点；若当前 3 个数的和大于 target，说明和不够大，则`k--`，即让第三个数小一点；如果当前 3 个数的和等于 target，直接返回和 。重复这个操作直到`j === k`


## 代码
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function (nums, target) {
  const n = nums.length - 1
  nums.sort((a, b) => a - b)
  let res = Number.POSITIVE_INFINITY
  for (let i = 0; i <= n; i++) {
    let j = i + 1
    let k = n
    while (j < k) {
      let sum = nums[i] + nums[j] + nums[k]
      res = Math.abs(sum - target) < Math.abs(res - target) ? sum : res
      if (sum < target) {
        j++
      } else if (sum > target) {
        k--
      } else {
        return res
      }
    }
  }
  return res
};
```

时间复杂度：`O(n^2)`