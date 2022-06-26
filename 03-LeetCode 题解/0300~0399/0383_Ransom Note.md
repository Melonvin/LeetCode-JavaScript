# [383. Ransom Note](https://leetcode.cn/problems/ransom-note/)
## 题目
Given two strings `ransomNote` and `magazine`, return `true`<em> if </em>`ransomNote`<em> can be constructed by using the letters from </em>`magazine`<em> and </em>`false`<em> otherwise</em>.

Each letter in `magazine` can only be used once in `ransomNote`.

 

<strong>Example 1:</strong>

```
Input: ransomNote = "a", magazine = "b"
Output: false
```

<strong>Example 2:</strong>

```
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

<strong>Example 3:</strong>

```
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

 

<strong>Constraints:</strong>


- `1 <= ransomNote.length, magazine.length <= 10^5`
- `ransomNote` and `magazine` consist of lowercase English letters.



## 题目大意
判断 `ransomNote` 中的每个字母是否都能在 `magazine` 找到相同字母，并且  `magazine` 中的每个字母只能使用一次

## 解题思路
1. 使用一个长度为 26 的数组统计 `magazine` 中每种字母出现的个数
2. 遍历 `ransomNote`，将统计数组中对应字母的个数减一，若减一后的个数小于零，则返回 false


## 代码
`TypeScript`
```TypeScript
function canConstruct(ransomNote: string, magazine: string): boolean {
  const n = ransomNote.length;
  const m = magazine.length;
  if (n > m) return false;

  const count: number[] = new Array(26).fill(0);
  for (let i = 0; i < m; i++) {
    count[magazine.charCodeAt(i) - 97]++;
  }

  for (let i = 0; i < n; i++) {
    const index: number = ransomNote.charCodeAt(i) - 97;
    count[index]--;
    if (count[index] < 0) {
      return false;
    }
  }
  return true;
}
```

`JavaScript`
```JavaScript
function canConstruct(ransomNote, magazine) {
  const n = ransomNote.length;
  const m = magazine.length;
  if (n > m) return false;
  const count = new Array(26).fill(0);
  for (let i = 0; i < m; i++) {
    count[magazine.charCodeAt(i) - 97]++;
  }
  for (let i = 0; i < n; i++) {
    const index = ransomNote.charCodeAt(i) - 97;
    count[index]--;
    if (count[index] < 0) {
      return false;
    }
  }
  return true;
}
```

## 复杂度分析
1. 时间复杂度：`O(n + m)`，最坏情况需遍历两个字符串
2. 空间复杂度：`O(C)`，C = 26