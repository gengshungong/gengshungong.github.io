---
layout: post
title: 一切离不开算法!
permalink: /algorithm/
---

* content
{:toc}

#### 基于学习 javascript 数据结构与算法一书的算法知识整理

`斐波那契数列`

> 原理：从第三项开始，每一项等于前两项的和

```js
function fibonac(num) {
  let fibonacci = [1, 2]
  for (let i = 1; i < fibonacci.length; i++) {
    fibonacci.push(fibonacci[i] + fibonacci[i - 1])
    if (num > 2 && i === num) {
      return fibonacci[i - 1]
    } else if (num === 1) {
      return 1
    } else if (num === 2) {
      return 2
    }
  }
}
```

##### 栈及其各个方法的封装(使用 es6 语法)

```js
class Stack {
  constructor() {
    this.arr = []
  }
  push = element => {
    return this.arr.push(element)
  }
  pop = () => {
    return this.arr.pop()
  }
  peek = () => {
    return this.arr[this.arr.length - 1]
  }
  isEmpty = () => {
    return this.arr.length === 0
  }
  size = () => {
    return this.arr.length
  }
  clear = () => {
    return (this.arr = [])
  }
}
```

`案例`

> 将一个值转为进制数 decNumber 为值 base 为进制类型,比如 2,8,16

```js
const baseConverter = (decNumber, base) => {
  let remStack = new Stack(),
    rem,
    baseString = '',
    digits = '0123456789ABCDEF'
  while (decNumber > 0) {
    rem = Math.floor(decNumber % base)
    remStack.push(rem)
    decNumber = Math.floor(decNumber / base)
  }
  while (!remStack.isEmpty()) {
    baseString += digits[remStack.pop()]
  }
  return baseString
}
```

##### 队列

```js
class Queue {
  constructor() {
    this.arr = []
  }
  enqueue = element => {
    return this.arr.push(element)
  }
  dequeue = () => {
    return this.arr.shift()
  }
  front = () => {
    return this.arr[0]
  }
  isEmpty = () => {
    return this.arr.length === 0
  }
  size = () => {
    return this.arr.length
  }
}
```

`案例`

> 优先队列

```js
class QueueElement {
  constructor(element, priority) {
    this.element = element
    this.priority = priority
  }
}
const items = []
class PriorityQueue {
  enqueue = (element, priority) => {
    let queueElement = new QueueElement(element, priority)
    if (!items.length) {
      items.push(queueElement)
    } else {
      let added = false
      for (const i in items) {
        if (queueElement.priority < items[i].priority) {
          items.splice(i, 0, queueElement)
          added = true
          break
        }
      }
      if (!added) {
        items.push(queueElement)
      }
    }
    return items
  }
}
```

> 击鼓传花游戏

```js
const hotPotato = (nameList, num) => {
  const queue = new Queue()
  for (const i in nameList) {
    queue.enqueue(nameList[i])
  }
  console.log(queue.size())
  let eliminated = ''
  while (queue.size() > 1) {
    for (let i = 0; i < num; i++) {
      queue.enqueue(queue.dequeue())
    }
    eliminated = queue.dequeue()
    console.log(eliminated + '在击鼓传花游戏中被淘汰。')
  }
  return queue.dequeue()
}
```

##### 单链表

```js
function LinkedList() {
  var Node = function(element) {
    this.element = element
    this.next = null
  }
  var length = 0
  var head = null
  // 尾部添加一个元素
  LinkedList.prototype.append = function(element) {
    var node = new Node(element),
      current
    if (head === null) {
      //列表中第一个节点
      head = node
    } else {
      current = head
      //循环列表，直到找到最后一项
      while (current.next) {
        current = current.next
      }
      //找到最后一项，将其next赋为node，建立连接
      current.next = node
    }
    length++ //更新列表的长度
  }

  // 移除某个元素
  LinkedList.prototype.removeAt = function(position) {
    //检查越界值
    if (position > -1 && position < length) {
      // {1}
      var current = head, // {2}
        previous, // {3}
        index = 0 // {4}
      //移除第一项
      if (position === 0) {
        // {5}
        head = current.next
      } else {
        while (index++ < position) {
          // {6}
          previous = current // {7}
          current = current.next // {8}
        }
        //将previous与current的下一项链接起来:跳过current，从而移除它
        previous.next = current.next // {9}
      }
      length-- // {10}
      return current.element
    } else {
      return null // {11}
    }
  }
  // 插入元素
  LinkedList.prototype.insert = function(position, element) {
    //检查越界值
    if (position >= 0 && position <= length) {
      //{1}
      var node = new Node(element),
        current = head,
        previous,
        index = 0
      if (position === 0) {
        //在第一个位置添加
        node.next = current
        head = node
      } else {
        while (index++ < position) {
          previous = current
          current = current.next
        }
        node.next = current
        previous.next = node
      }
      length++ //更新列表的长度
      return true
    } else {
      return false //{6}
    }
  }
  // toString()
  LinkedList.prototype.toString = function() {
    var current = head,
      string = ''
    while (current) {
      string = current.element
      current = current.next
    }
    return string //{6}
  }
  // get获取某个位置的数据
  LinkedList.prototype.get = function(position) {
    // 越界判断
    if (position >= 0 || position < length) {
      var current = head
      // head.next = current
      var index = 0
      while (index++ < position) {
        current = current.next
      }
      return current.element
    }
  }

  // indexOf()
  LinkedList.prototype.indexOf = function(element) {
    var current = head, //{1}
      index = -1
    while (current) {
      //{2}
      if (element === current.element) {
        return index //{3}
      }
      index++ //{4}
      current = current.next //{5}
    }
    return -1
  }

  // 更新某个位置的数据
  LinkedList.prototype.update = function(newElement, position) {
    if (position >= 0 || position < length) {
      var current = head
      var index = 0
      while (index++ < position) {
        current = current.next
      }
      current.element = newElement
      // 修改成功标识
      return true
    }
  }

  // 删除某个数据
  LinkedList.prototype.remove = function(element) {
    var position = this.indexOf(element)
    return this.removeAt(position)
  }
}
```
