# [1. Two Sum](https://leetcode-cn.com/problems/two-sum/)
## 题目
Given an array of integers `nums` and an integer `target`, return <em>indices of the two numbers such that they add up to `target`</em>.

You may assume that each input would have <strong><em>exactly</em> one solution</strong>, and you may not use the <em>same</em> element twice.

You can return the answer in any order.

 

<strong>Example 1:</strong>

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

<strong>Example 2:</strong>

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

<strong>Example 3:</strong>

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

 

<strong>Constraints:</strong>


- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- <strong>Only one valid answer exists.</strong>

## 题目大意

在给定整数数组`nums`中找到两个数的和为`target`，返回这两个数的索引

## 解题思路

### 方法一：暴力枚举

时间复杂度为`O(n^2)`

### 方法二

遍历数组，对每一个元素`nums[i]`，我们用 Map 来保存和它有关的信息：用 `target - nums[i]`作为 key，用 `i`作为 value 

这样访问某个元素时，即可在 Map 中查询已遍历元素中是否有和它配对的元素（即和为`target`）

## 代码

### 方法一

略

### 方法二

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
    let map = new Map();
    for (let i = 0, len = nums.length; i < len; i++) {
        if (map.has(target - nums[i])) {
            return [map.get(target - nums[i]), i];
        } else {
            map.set(nums[i], i);
        }
    }
    return [];
};
```

时间复杂度：`O(N)`，N 为数组长度

空间复杂度：`O(N)`，使用了 Map 来存储