# [710. Random Pick with Blacklist](https://leetcode.cn/problems/random-pick-with-blacklist/)
## 题目
You are given an integer `n` and an array of <strong>unique</strong> integers `blacklist`. Design an algorithm to pick a random integer in the range `[0, n - 1]` that is <strong>not</strong> in `blacklist`. Any integer that is in the mentioned range and not in `blacklist` should be <strong>equally likely</strong> to be returned.

Optimize your algorithm such that it minimizes the number of calls to the <strong>built-in</strong> random function of your language.

Implement the `Solution` class:


- `Solution(int n, int[] blacklist)` Initializes the object with the integer `n` and the blacklisted integers `blacklist`.
- `int pick()` Returns a random integer in the range `[0, n - 1]` and not in `blacklist`.


 

<strong>Example 1:</strong>

```
Input
["Solution", "pick", "pick", "pick", "pick", "pick", "pick", "pick"]
[[7, [2, 3, 5]], [], [], [], [], [], [], []]
Output
[null, 0, 4, 1, 6, 1, 0, 4]

Explanation
Solution solution = new Solution(7, [2, 3, 5]);
solution.pick(); // return 0, any integer from [0,1,4,6] should be ok. Note that for every call of pick,
                 // 0, 1, 4, and 6 must be equally likely to be returned (i.e., with probability 1/4).
solution.pick(); // return 4
solution.pick(); // return 1
solution.pick(); // return 6
solution.pick(); // return 1
solution.pick(); // return 0
solution.pick(); // return 4
```

 

<strong>Constraints:</strong>


- `1 <= n <= 10^9`
- `0 <= blacklist.length <= min(10^5, n - 1)`
- `0 <= blacklist[i] < n`
- All the values of `blacklist` are <strong>unique</strong>.
- At most `2 * 10^4` calls will be made to `pick`.



## 题目大意

在 `[0, n - 1]` 的范围中有若干个数被列为黑名单，设计一种算法，调用最少次数的内置 random 方法，从 `[0, n - 1]` 随机取出一个不在黑名单中的数

## 解题思路
1. 设黑名单的长度为 m
2. 可以通过一次 Math.random 方法得到 [0, n - m) 中的一个数
3. 使用 map 将 [0, n - m) 中的“黑名单数”映射为 [n - m, n - 1] 中的非“黑名单数”

## 代码
`TypeScript`
```ts
class Solution {
  blackToWhite: Map<number, number> = new Map<number, number>();
  bound: number;
  constructor(n: number, blacklist: number[]) {
    this.init(n, blacklist);
  }

  init(n: number, blacklist: number[]) {
    const m = blacklist.length;
    this.bound = n - m;
    const set = new Set<number>();
    blacklist.forEach((item) => {
      if (item >= this.bound) {
        set.add(item);
      }
    });
    let j = this.bound;
    blacklist.forEach((item) => {
      if (item < this.bound) {
        while (set.has(j)) j++;
        this.blackToWhite.set(item, j);
        j++;
      }
    });
  }

  pick(): number {
    const random = Math.floor(Math.random() * this.bound);
    return this.blackToWhite.get(random) || random;
  }
}

/**
 * Your Solution object will be instantiated and called as such:
 * var obj = new Solution(n, blacklist)
 * var param_1 = obj.pick()
 */

```

`JavaScript`
```JavaScript
function Solution(n, blacklist) {
  this.blackToWhite = new Map();
  this.init(n, blacklist);
}
Solution.prototype.init = function (n, blacklist) {
  var _this = this;
  var m = blacklist.length;
  this.bound = n - m;
  var set = new Set();
  blacklist.forEach(function (item) {
    if (item >= _this.bound) {
      set.add(item);
    }
  });
  var j = this.bound;
  blacklist.forEach(function (item) {
    if (item < _this.bound) {
      while (set.has(j)) j++;
      _this.blackToWhite.set(item, j);
      j++;
    }
  });
};
Solution.prototype.pick = function () {
  var random = Math.floor(Math.random() * this.bound);
  return this.blackToWhite.get(random) || random;
};
return Solution;

/**
 * Your Solution object will be instantiated and called as such:
 * var obj = new Solution(n, blacklist)
 * var param_1 = obj.pick()
 */
```
## 复杂度分析
1. 时间复杂度：映射 `O(m)`，pick `O(1)`
2. 空间复杂度：`O(m)` 最多存储 m 个黑名单数的映射
