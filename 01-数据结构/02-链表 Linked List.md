# 链表

## 1 基本介绍

数组这种数据结构最大的缺点：从数组的起点或中间插入或移出项的成本很高，因为需要移动元素

和数组一样，**链表**也存储有序（这里指前后顺序，不是大小顺序）的元素集合

不同于数组，**链表**中的元素在内存中并不是连续放置

**链表**的每个元素由一个存储元素本身的节点和一个指向下一个元素的引用组成（如下图所示）

![图片](https://melonvin-1302080640.cos.ap-shanghai.myqcloud.com/%E5%9B%BE%E7%89%87.png)

链表的特点：

1. 添加或移除元素不需要移动其他元素
2. 访问元素需要从链表头开始遍历直到找到所需的元素

## 2 JS 实现

理解原理，实际工作基本不会用到

### 2.1 单向链表

```js
/**
 * @description 节点
 */
class Node {
  constructor(element) {
    this.element = element
    this.next = undefined
  }
}

/**
 * @description 单向链表
 */
class LinkedList {
  constructor() {
    this.count = 0
    this.head = undefined
  }

  // 链表尾部添加元素
  push(element) {
    const node = new Node(element)
    let current
    if (!this.head) {
      this.head = node
    } else {
      let current = this.head
      while (!current.next) {
        current = current.next
      }
      current.next = node
    }
    this.count++
  }

  // 获取目标索引处节点，从 0 开始
  getElementAt(index) {
    if (index >= 0 && index < this.count) {
      let current = this.head
      for (let i = 0; i < index && current != null; i++) {
        current = current.next
      }
      return current
    }
    return undefined
  }

  // 移除节点
  removeAt(index) {
    if (index >= 0 && index < this.count) {
      let current = this.head
      if (index === 0) {
        this.head = current.next
      } else {
        const previous = this.getElementAt(index - 1)
        current = previous.next
        previous.next = current.next
      }
      this.count--
    }
    return undefined
  }

  // 插入节点
  insert(element, index) {
    if (index >= 0 && index <= this.count) {
      const node = new Node(element)
      if (index === 0) {
        node.next = this.head
        this.head = node
      } else {
        const previous = this.getElementAt(index - 1)
        const current = previous.next
        node.next = current
        previous.next = node
      }
      this.count++
      return true
    }
    return false
  }

  // 返回元素的位置
  indexOf(element) {
    let current = this.head
    for (let i = 0; i < this.count && current != null; i++) {
      if (current.element === element) {
        return i
      }
      current = current.next
    }
    return -1
  }

  // 移除元素
  remove(element) {
    const index = this.indexOf(element)
    return this.removeAt(index)
  }

  // 链表长度
  size() {
    return this.count
  }

  // 判断是否为空
  isEmpty() {
    return this.size() === 0
  }

  // 获取链表头
  getHead() {
    return this.head
  }
}
```

### 2.2 双向链表

**双向链表**和普通链表的区别在于，在链表中，一个节点只有链向下一个节点的链接；而在双向链表中，链接是双向的：一个链向下一个元素，另一个链向前一个元素，如下图所示。

![图片1](https://melonvin-1302080640.cos.ap-shanghai.myqcloud.com/%E5%9B%BE%E7%89%871.png)

```js
/**
 * @description 双向链表节点
 */
class DoublyNode extends Node {
  constructor(element, next, prev) {
    super(element, next)
    this.prev = prev
  }
}

/**
 * @description 双向链表
 */
class DoublyLinkedList extends LinkedList {
  constructor() {
    super()
    // 表尾
    this.tail = undefined
  }

  /**
   * @description 在任意位置插入元素
   * @param {*} element 
   * @param {number} index 
   * @returns {boolean} 是否插入成功
   */
  insert(element, index) {
    if (index >= 0 && index <= this.count) {
      const node = new DoublyNode(element)
      let current = this.head
      if (index === 0) {
        if (this.head == null) {
          this.head = node
          this.tail = node
        } else {
          node.next = this.head
          current.prev = node
          this.head = node
        }
      } else if (index === this.count) {
        current = this.tail
        current.next = node
        node.prev = current
        this.tail = node
      } else {
        const previous = this.getElementAt(index - 1)
        current = previous.next
        node.next = current
        previous.next = node
        current.prev = node
        node.prev = previous
      }
      this.count++
      return true
    }
    return false
  }

  /**
   * @description 从任意位置移除元素
   * @param {number} index 
   * @returns 移除元素
   */
  removeAt(index) {
    if (index >= 0 && index < this.count) {
      let current = this.head
      if (index === 0) {
        this.head = current.next
        if (this.count === 1) {
          this.tail = undefined
        } else {
          this.head.prev = undefined
        }
      } else if (index === this.count - 1) {
        current = this.tail
        this.tail = current.prev
        this.tail.next = undefined
      } else {
        current = this.getElementAt(index)
        const previous = current.prev
        previous.next = current.next
        current.next.prev = previous
      }
      this.count--
      return current.element
    }
    return undefined
  }
}
```

### 2.3 循环链表

单向循环链表和单向链表的唯一区别在于，最后一个元素指向第一个元素（head），如图所示

![图片2](https://melonvin-1302080640.cos.ap-shanghai.myqcloud.com/%E5%9B%BE%E7%89%872.png)

同理，**双向循环链表**有指向 head 元素的 tail.next 和指向 tail 元素的 head.prev。

![图片3](https://melonvin-1302080640.cos.ap-shanghai.myqcloud.com/%E5%9B%BE%E7%89%873.png)

```js
/**
 * @description 单向循环链表
 */
class CircularLinkedList extends LinkedList {
  constructor() {
    super()
  }

  /**
   * @description 在任意位置插入元素
   * @param {*} element 
   * @param {number} index 
   * @returns {boolean} 是否插入成功
   */
  insert(element, index) {
    if (index >= 0 && index <= this.count) {
      const node = new Node(element)
      let current = this.head
      if (index === 0) {
        if (this.head == null) {
          this.head = node
          node.next = this.head
        } else {
          node.next = current
          current = this.getElementAt(this.size() - 1)
          this.head = node
          current.next = this.head
        }
      } else {
        const previous = this.getElementAt(index - 1)
        node.next = previous.next
        previous.next = node
      }
      this.count++
      return true
    }
    return false
  }

  /**
   * @description 从任意位置移除元素
   * @param {number} index 
   * @returns 移除元素
   */
  removeAt(index) {
    if (index >= 0 && index < this.count) {
      let current = this.head
      if (index === 0) {
        if (this.count === 1) {
          this.head = undefined
        } else {
          const removed = this.head
          current = this.getElementAt(this.size() - 1)
          this.head = this.head.next
          current.next = this.head
          current = removed
        }
      } else {
        const previous = this.getElementAt(index - 1)
        current = previous.next
        previous.next = current.next
      }
      this.count--
      return current.element
    }
    return undefined
  }
}
```



### 2.4 有序链表

**有序链表**是指保持元素有序的链表结构，在插入元素时比较大小来确定插入位置

## 3 题目列表

### 3.1 简单题

| No.  | Title                                                |                        Solution                         | Difficulty |
| :--: | :--------------------------------------------------- | :-----------------------------------------------------: | :--------: |
| 0001 | [Two Sum](https://leetcode-cn.com/problems/two-sum/) | [JS](../03-LeetCode%20题解/0001~0099/0001.Two%20Sum.md) |    Easy    |

### 3.2 中等题

| No.  | Title                                                        |                           Solution                           | Difficulty |
| :--: | :----------------------------------------------------------- | :----------------------------------------------------------: | :--------: |
| 0015 | [3Sum](https://leetcode-cn.com/problems/3sum/)               |      [JS](../03-LeetCode%20题解/0001~0099/0015.3Sum.md)      |   Medium   |
| 0016 | [3Sum Closest](https://leetcode-cn.com/problems/3sum-closest/) | [JS](../03-LeetCode%20题解/0001~0099/0016.3Sum%20Closest.md) |   Medium   |
| 0018 | [4Sum](https://leetcode-cn.com/problems/4sum/)               |      [JS](../03-LeetCode%20题解/0001~0099/0018.4Sum.md)      |   Medium   |

