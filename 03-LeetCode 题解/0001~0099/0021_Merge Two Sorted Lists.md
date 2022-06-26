# [21. Merge Two Sorted Lists](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
## 题目
You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists in a one <strong>sorted</strong> list. The list should be made by splicing together the nodes of the first two lists.

Return <em>the head of the merged linked list</em>.

 

<strong>Example 1:</strong>



```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

<strong>Example 2:</strong>

```
Input: list1 = [], list2 = []
Output: []
```

<strong>Example 3:</strong>

```
Input: list1 = [], list2 = [0]
Output: [0]
```

 

<strong>Constraints:</strong>


- The number of nodes in both lists is in the range `[0, 50]`.
- `-100 <= Node.val <= 100`
- Both `list1` and `list2` are sorted in <strong>non-decreasing</strong> order.



## 题目大意

将两个有序链表合并成一个有序链表

## 解题思路

### 方法1：迭代

1. 创建一个新链表的头结点`head`，最后返回`head.next`
2. 维护一个指针`prev`，初始时`prev = head`
3. 比较`list1`、`list2`的值，将较小节点接在`prev`之后
4. 后移`list1`或`list2`（步骤 3 中比较谁小就移动谁），后移`prev`
5. 重复步骤 3、4 直到遍历完`list1`和`list2`之一，将两者剩余节点接在`prev`之后

### 方法2：递归

终止条件：两个链表有一个为空

递归过程：比较两个链表的头节点，设较小节点为`node`，让`node.next`指向`mergeTwoLists(node.next, 另一个链表)`

## 代码

### 迭代

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function (list1, list2) {
  let head = new ListNode(-1)
  let prev = head
  while (list1 != null && list2 != null) {
    if (list1.val < list2.val) {
      prev.next = list1
      list1 = list1.next
    } else {
      prev.next = list2
      list2 = list2.next
    }
    prev = prev.next
  }
  prev.next = list1 == null ? list2 : list1
  return head.next
};
```

时间复杂度：`O(n + m)`，n、m 分别为两个链表的长度

空间复杂度：`O(1)`

### 递归

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 *
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function (list1, list2) {
  if (list1 == null) return list2;
  if (list2 == null) return list1;
  if (list1.val < list2.val) {
    list1.next = mergeTwoLists(list1.next, list2);
    return list1;
  } else {
    list2.next = mergeTwoLists(list1, list2.next);
    return list2;
  }
};
```

时间复杂度：`O(n + m)`

空间复杂度：`O(n + m)`