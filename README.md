# blog


前言
数据结构是计算机存储、组织数据的方式,算法是系统描述解决问题的策略。了解基本的数据结构和算法可以提高代码的性能和质量。
也是程序猿进阶的一个重要技能。
手撸代码实现栈,队列,链表,字典,二叉树,动态规划和贪心算法
1.数据结构篇
### 1.1 栈
栈的特点：先进后出
```
class Stack {
    constructor() {
      this.items = [];
    }

    // 入栈
    push(element) {
      this.items.push(element);
    }

    // 出栈
    pop() {
      return this.items.pop();
    }

    // 末位
    get peek() {
      return this.items[this.items.length - 1];
    }

    // 是否为空栈
    get isEmpty() {
      return !this.items.length;
    }

    // 长度
    get size() {
      return this.items.length;
    }

    // 清空栈
    clear() {
      this.items = [];
    }
  }

  // 实例化一个栈
  const stack = new Stack();
  console.log(stack.isEmpty); // true

  // 添加元素
  stack.push(5);
  stack.push(8);

  // 读取属性再添加
  console.log(stack.peek); // 8
  stack.push(11);
  console.log(stack.size); // 3
  console.log(stack.isEmpty); // false
```
1.2 队列
队列：先进先出
```
  class Queue {
    constructor(items) {
      this.items = items || [];
    }

    enqueue(element) {
      this.items.push(element);
    }

    dequeue() {
      return this.items.shift();
    }

    front() {
      return this.items[0];
    }

    clear() {
      this.items = [];
    }

    get size() {
      return this.items.length;
    }

    get isEmpty() {
      return !this.items.length;
    }

    print() {
      console.log(this.items.toString());
    }
  }

  const queue = new Queue();
  console.log(queue.isEmpty); // true

  queue.enqueue("John");
  queue.enqueue("Jack");
  queue.enqueue("Camila");
  console.log(queue.size); // 3
  console.log(queue.isEmpty); // false
  queue.dequeue();
  queue.dequeue();
```
1.3 链表
链表:存贮有序元素的集合,
但是不同于数组,每个元素是一个存贮元素本身的节点和指向下一个元素引用组成
要想访问链表中间的元素,需要从起点开始遍历找到所需元素

```
class Node {
    constructor(element) {
      this.element = element;
      this.next = null;
    }
  }

  // 链表
  class LinkedList {
    constructor() {
      this.head = null;
      this.length = 0;
    }

    // 追加元素
    append(element) {
      const node = new Node(element);
      let current = null;
      if (this.head === null) {
        this.head = node;
      } else {
        current = this.head;
        while (current.next) {
          current = current.next;
        }
        current.next = node;
      }
      this.length++;
    }

    // 任意位置插入元素
    insert(position, element) {
      if (position >= 0 && position <= this.length) {
        const node = new Node(element);
        let current = this.head;
        let previous = null;
        let index = 0;
        if (position === 0) {
          this.head = node;
        } else {
          while (index++ < position) {
            previous = current;
            current = current.next;
          }
          node.next = current;
          previous.next = node;
        }
        this.length++;
        return true;
      }
      return false;
    }

    // 移除指定位置元素
    removeAt(position) {
      // 检查越界值
      if (position > -1 && position < length) {
        let current = this.head;
        let previous = null;
        let index = 0;
        if (position === 0) {
          this.head = current.next;
        } else {
          while (index++ < position) {
            previous = current;
            current = current.next;
          }
          previous.next = current.next;
        }
        this.length--;
        return current.element;
      }
      return null;
    }

    // 寻找元素下标
    findIndex(element) {
      let current = this.head;
      let index = -1;
      while (current) {
        if (element === current.element) {
          return index + 1;
        }
        index++;
        current = current.next;
      }
      return -1;
    }

    // 删除指定文档
    remove(element) {
      const index = this.indexOf(element);
      return this.removeAt(index);
    }

    isEmpty() {
      return !this.length;
    }

    size() {
      return this.length;
    }

    // 转为字符串
    toString() {
      let current = this.head;
      let string = "";
      while (current) {
        string += ` ${current.element}`;
        current = current.next;
      }
      return string;
    }
  }
  const linkedList = new LinkedList();

  console.log(linkedList);
  linkedList.append(2);
  linkedList.append(6);
  linkedList.append(24);
  linkedList.append(152);

  linkedList.insert(3, 18);
  console.log(linkedList);
  console.log(linkedList.findIndex(24));  
``` 
1.4 字典
字典：类似对象，以key，value存贮值
```
class Dictionary {
    constructor() {
      this.items = {};
    }

    set(key, value) {
      this.items[key] = value;
    }

    get(key) {
      return this.items[key];
    }

    remove(key) {
      delete this.items[key];
    }

    get keys() {
      return Object.keys(this.items);
    }

    get values() {
      /*
    也可以使用ES7中的values方法
    return Object.values(this.items)
    */

      // 在这里我们通过循环生成一个数组并输出
      return Object.keys(this.items).reduce((r, c, i) => {
        r.push(this.items[c]);
        return r;
      }, []);
    }
  }
  const dictionary = new Dictionary();
  dictionary.set("Gandalf", "gandalf@email.com");
  dictionary.set("John", "johnsnow@email.com");
  dictionary.set("Tyrion", "tyrion@email.com");

  console.log(dictionary);
  console.log(dictionary.keys);
  console.log(dictionary.values);
  console.log(dictionary.items);
```
1.5 二叉树
特点：每个节点最多有两个子树的树结构
```
class NodeTree {
    constructor(key) {
      this.key = key;
      this.left = null;
      this.right = null;
    }
  }

  class BinarySearchTree {
    constructor() {
      this.root = null;
    }

    insert(key) {
      const newNode = new NodeTree(key);
      const insertNode = (node, newNode) => {
        if (newNode.key < node.key) {
          if (node.left === null) {
            node.left = newNode;
          } else {
            insertNode(node.left, newNode);
          }
        } else {
          if (node.right === null) {
            node.right = newNode;
          } else {
            insertNode(node.right, newNode);
          }
        }
      };
      if (!this.root) {
        this.root = newNode;
      } else {
        insertNode(this.root, newNode);
      }
    }

    //访问树节点的三种方式:中序,先序,后序
    inOrderTraverse(callback) {
      const inOrderTraverseNode = (node, callback) => {
        if (node !== null) {
          inOrderTraverseNode(node.left, callback);
          callback(node.key);
          inOrderTraverseNode(node.right, callback);
        }
      };
      inOrderTraverseNode(this.root, callback);
    }

    min(node) {
      const minNode = node => {
        return node ? (node.left ? minNode(node.left) : node) : null;
      };
      return minNode(node || this.root);
    }

    max(node) {
      const maxNode = node => {
        return node ? (node.right ? maxNode(node.right) : node) : null;
      };
      return maxNode(node || this.root);
    }
  }
  const tree = new BinarySearchTree();
  tree.insert(11);
  tree.insert(7);
  tree.insert(5);
  tree.insert(3);
  tree.insert(9);
  tree.insert(8);
  tree.insert(10);
  tree.insert(13);
  tree.insert(12);
  tree.insert(14);
  tree.inOrderTraverse(value => {
    console.log(value);
  });

  console.log(tree.min());
  console.log(tree.max());
```
2.算法篇
2.1 冒泡算法
冒泡排序，选择排序，插入排序，此处不做赘述，请戳 排序

2.2 斐波那契
特点：第三项等于前面两项之和
```
function fibonacci(num) { 
    if (num === 1 || num === 2) { 
        return 1
    }
    return fibonacci(num - 1) + fibonacci(num - 2)
  }
```
2.3 动态规划
特点：通过全局规划,将大问题分割成小问题来取最优解
案例：最少硬币找零
美国有以下面额(硬币）：d1=1, d2=5, d3=10, d4=25
如果要找36美分的零钱，我们可以用1个25美分、1个10美分和1个便士（ 1美分)

class MinCoinChange {

constructor(coins) {
    this.coins = coins
    this.cache = {}
}

makeChange(amount) {
    if (!amount) return []
    if (this.cache[amount]) return this.cache[amount]
    let min = [], newMin, newAmount
    this.coins.forEach(coin => {
        newAmount = amount - coin
        if (newAmount >= 0) {
            newMin = this.makeChange(newAmount)
        }
        if (newAmount >= 0 && 
             (newMin.length < min.length - 1 || !min.length) && 
             (newMin.length || !newAmount)) {
            min = [coin].concat(newMin)
        }
    })
    return (this.cache[amount] = min)
}
}
```
const rninCoinChange = new MinCoinChange([1, 5, 10, 25])
console.log(rninCoinChange.makeChange(36))
// [1, 10, 25]
const minCoinChange2 = new MinCoinChange([1, 3, 4])
console.log(minCoinChange2.makeChange(6))
// [3, 3]
2.4 贪心算法
特点：通过最优解来解决问题
用贪心算法来解决2.3中的案例
```
class MinCoinChange2 {

constructor(coins) {
    this.coins = coins
}

makeChange(amount) {
    const change = []
    let total = 0
    this.coins.sort((a, b) => a < b).forEach(coin => {
        if ((total + coin) <= amount) {
            change.push(coin)
            total += coin
        }
    })
    return change
}
}
const rninCoinChange2 = new MinCoinChange2 ( [ 1, 5, 10, 25])
console.log (rninCoinChange2. makeChange (36))
```