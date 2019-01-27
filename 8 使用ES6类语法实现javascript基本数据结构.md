使用ES6类语法实现javasript数据结构
====================================

## 目录
- [栈](#栈)
- [队列](#队列)
- [链表](#链表)
- [集合](#集合)
- [字典](#字典)
- [散列表](#散列表)
- [树](#树)
- [图](#图)

## 栈
```
class Stack {
  //  保存栈中的元素
  constructor(...items) {
    this._items = [];

    if (items.length > 0) {
      items.forEach(item => this._items.push(item));
    }
  }

  //  向栈中添加元素
  push(...items) {
    items.forEach(item => this._items.push(item));
    return this._items;
  }

  //  从栈中移除元素
  pop(count = 0) {
    if (count === 0) {
      return this._items.pop();
    } else {
      return this._items.splice(-count, count);
    }
  }

  //  查看栈顶元素
  peek() {
    console.log(this._items[this._items.length - 1]);
  }

  //检查栈是否为空
  isEmpty() {
    return this._items.length === 0;
  }

  //  打印所有栈元素
  print() {
    this._items.forEach(item => {
      console.log(item.toString());
    });
  }

  //  清空栈元素
  clear() {
    this._items = [];
  }
}

//  初始化一个栈
let stack = new Stack(1, 24, 4); // [1,24,4]

//  向栈中添加元素
stack.push(5, 6); // [1,24,4,5,6]

//  从栈中移除元素
stack.pop(2); // [1,24,4]

//  查看栈顶元素
stack.peek(); // 4

// 查看栈是否为空
let isEmpty = stack.isEmpty(); // false

//  打印所有栈元素
stack.print(); // 1, 24, 4

//  清空栈
stack.clear(); // []

```
## 队列
```
class Queue {
  //  初始化队列
  constructor(...items) {
    this._items = [];
    this.enqueue(...items);
  }

  //  入列
  enqueue(...items) {
    items.forEach(item => this._items.push(item));
    return this._items;
  }

  //  出列
  dequeue(count = 1) {
    this._items.splice(0, count);
    return this._items;
  }

  //  查看栈顶元素
  peek() {
    return this._items[0];
  }

  //  获取队列的长度
  size() {
    return this._items.length;
  }

  //  检查队列是否为空
  isEmpty() {
    return this._items.length === 0;
  }
}
let my_queue = new Queue(1, 24, 4); // [1, 24, 4]

my_queue.enqueue(23); // [1, 24, 4, 23]

my_queue.enqueue(1, 2, 342); //[1, 24, 4, 23, 1, 2, 342]

my_queue.dequeue(); //[24, 4, 23, 1, 2, 342]

my_queue.dequeue(3); //[1, 2, 342]

my_queue.isEmpty(); // false

my_queue.size(); //3

```
## 链表
## 集合
## 字典
## 散列表
## 树
## 图
