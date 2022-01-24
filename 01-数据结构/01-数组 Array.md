# 数组

## 1 知识汇总

数组是最简单的内存数据结构，数据结构的基本操作无非”遍历+访问”，展开讲就是“增删改查”

下面列出 JavaScript 中处理数组最常用的方法

> 工作中灵活运用，部分方法刷题慎用。

比如题目考察的就是排序，就不要用`sort`了，如果排序只是解题的一小步，那就没必要自己再写一遍排序了，直接用`sort`

## 1.1 基本方法

**增**

| 方法                                                         | 描述         | 语法                                            |
| :----------------------------------------------------------- | :----------- | ----------------------------------------------- |
| [push](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push) | 尾部添加     | `arr.push(element1, ..., elementN)`             |
| [unshift](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) | 头部添加     | `arr.unshift(element1, ..., elementN)`          |
| [splice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) | 任意位置添加 | `arr.splice(start, 0, element1, ..., elementN)` |

**删**

| 方法                                                                                                    | 描述                 | 语法                             |
| ------------------------------------------------------------------------------------------------------- | -------------------- | -------------------------------- |
| [pop](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)       | 删除**最后一个**元素 | `arr.pop()`                      |
| [shift](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)   | 删除**第一个**元素   | `arr.shift()`                    |
| [splice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) | 任意位置删除         | `arr.splice(start, deleteCount)` |

**改**

下标赋值

**查**

| 方法                                                         | 描述                                               | 语法                                          |
| ------------------------------------------------------------ | -------------------------------------------------- | --------------------------------------------- |
| [indexOf](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) | 返回第一个与给定参数相等的元素索引                 | `arr.indexOf(searchElement[, fromIndex])`     |
| [lastIndexOf](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf) | 返回最后一个与给定参数相等的元素索引               | `arr.lastIndexOf(searchElement[, fromIndex])` |
| [find](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/find) | 返回数组中满足提供的测试函数的第一个元素的值       | `arr.find(callback[, thisArg])`               |
| [findIndex](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) | 返回数组中满足提供的测试函数的第一个元素的**索引** | `arr.findIndex(callback[, thisArg])`          |
| [includes](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) | 判断数组是否包含一个指定的值                       | `arr.includes(valueToFind[, fromIndex])`      |

## 1.2 其他方法

**数组合并**

| 方法                                                         | 描述                               | 语法                                                         |
| ------------------------------------------------------------ | ---------------------------------- | ------------------------------------------------------------ |
| [concat](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) | 合并两个或多个数组，返回一个新数组 | `new_array = old_array.concat(value1[, value2[, ...[, valueN]]])` |

**迭代器函数**

| 方法                                                         | 描述                                                         | 语法                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [every](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every) | 测试一个数组内的所有元素是否都能通过某个指定函数的测试       | `arr.every(callback(element[, index[, array]])[, thisArg])`  |
| [some](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some) | 测试数组中是不是至少有1个元素通过了被提供的函数测试          | `arr.some(callback(element[, index[, array]])[, thisArg])`   |
| [forEach](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) | 遍历数组                                                     | `arr.forEach(callback(currentValue [, index [, array]])[, thisArg])` |
| [map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map) | 创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。 | `new_array = arr.map(function callback(currentValue[, index[, array]]) {  // Return element for new_array  }[, thisArg])` |
| [filter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) | 创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。   | `newArray = arr.filter(callback(element[, index[, array]])[, thisArg])` |
| [reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) | 对数组中的每个元素执行一个由您提供的**reducer**函数(升序执行)，将其结果汇总为单个返回值。 | `arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])` |

**排序方法**

| 方法                                                         | 描述               | 语法                          |
| ------------------------------------------------------------ | ------------------ | ----------------------------- |
| [reverse](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) | 反转数组           | `arr.reverse()`               |
| [sort](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) | 对数组元素进行排序 | `arr.sort([compareFunction])` |

## 2 题目列表

### 2.1 简单题

|  No.  | Title                                                |                        Solution                         | Difficulty |
| :---: | :--------------------------------------------------- | :-----------------------------------------------------: | :--------: |
| 0001  | [Two Sum](https://leetcode-cn.com/problems/two-sum/) | [JS](../03-LeetCode%20题解/0001~0099/0001.Two%20Sum.md) |    Easy    |

### 2.2 中等题

|  No.  | Title                                                          |                           Solution                           | Difficulty |
| :---: | :------------------------------------------------------------- | :----------------------------------------------------------: | :--------: |
| 0015  | [3Sum](https://leetcode-cn.com/problems/3sum/)                 |      [JS](../03-LeetCode%20题解/0001~0099/0015.3Sum.md)      |   Medium   |
| 0016  | [3Sum Closest](https://leetcode-cn.com/problems/3sum-closest/) | [JS](../03-LeetCode%20题解/0001~0099/0016.3Sum%20Closest.md) |   Medium   |
| 0018  | [4Sum](https://leetcode-cn.com/problems/4sum/)                 |      [JS](../03-LeetCode%20题解/0001~0099/0018.4Sum.md)      |   Medium   |

