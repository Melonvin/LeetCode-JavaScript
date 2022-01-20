# 数组

## 1 知识汇总

数组是最简单的内存数据结构，数据结构的基本操作无非”遍历+访问”，展开讲就是“增删改查”

### 1.1 增

| 方法                                                                                                      | 描述         | 语法                                            |
| :-------------------------------------------------------------------------------------------------------- | :----------- | ----------------------------------------------- |
| [push](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)       | 尾部添加     | `arr.push(element1, ..., elementN)`             |
| [unshift](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) | 头部添加     | `arr.unshift(element1, ..., elementN)`          |
| [splice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)   | 任意位置添加 | `arr.splice(start, 0, element1, ..., elementN)` |

### 1.2 删

| 方法                                                                                                    | 描述                 | 语法                             |
| ------------------------------------------------------------------------------------------------------- | -------------------- | -------------------------------- |
| [pop](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)       | 删除**最后一个**元素 | `arr.pop()`                      |
| [shift](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)   | 删除**第一个**元素   | `arr.shift()`                    |
| [splice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) | 任意位置删除         | `arr.splice(start, deleteCount)` |

### 1.3 改

## 2 题目列表

### 2.1 简单题

| No.  | Title                                                |                     Solution                     | Difficulty |
| :--: | :--------------------------------------------------- | :----------------------------------------------: | :--------: |
| 0001 | [Two Sum](https://leetcode-cn.com/problems/two-sum/) | [JS](../03-LeetCode 题解/0001~0099/0001.Two Sum) |    Easy    |

