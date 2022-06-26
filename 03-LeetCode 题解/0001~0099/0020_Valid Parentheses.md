# [20. Valid Parentheses](https://leetcode-cn.com/problems/valid-parentheses/)
## 题目
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:


- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.




<strong>Example 1:</strong>

```
Input: s = "()"
Output: true
```

<strong>Example 2:</strong>

```
Input: s = "()[]{}"
Output: true
```

<strong>Example 3:</strong>

```
Input: s = "(]"
Output: false
```

 

<strong>Constraints:</strong>


- `1 <= s.length <= 10^4`
- `s` consists of parentheses only `'()[]{}'`.



## 题目大意

判断给定字符串中的括号是否”对称“

## 解题思路

1. 遍历字符串，遇到左括号就把它对应的右括号入栈
2. 遇到右括号就判断与栈顶元素是否相同，栈为空或与栈顶元素不同，则字符串不“对称”
3. 遍历完毕，若栈不为空，则说明字符串不“对称”


## 代码
```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  const stack = []
  for (let c of s) {
    if (c === '(') {
      stack.push(')')
    } else if (c === '[') {
      stack.push(']')
    } else if (c === '{') {
      stack.push('}')
    } else if (stack.length === 0 || c !== stack.pop()) {
      return false
    }
  }
  return stack.length === 0
};
```

时间复杂度：`O(n)`

空间复杂度：`O(n)`