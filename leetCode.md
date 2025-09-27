# 数据结构
## 栈 Stack
**特点**：在 Python 中，栈一般用 列表 list 来实现，遵循 *后进先出（LIFO）* 原则
<img src="https://i-blog.csdnimg.cn/direct/adb97705f7e64b1da0e9139a16aa5be1.png#pic_center" width="450">

**操作**：
1. 创建空栈：`stack = []`
2. 压栈：`stack.append(元素)`
3. 出栈：`stack.pop()`
4. 查看栈顶元素：`stack[-1]`
5. 判断是否为空：`not stack`
6. 长度：`len(stack)`

## 队列 Queue
**特点**：遵循 *先进先出（FIFO）* 原则
<img src="https://i-blog.csdnimg.cn/direct/0f2c1fca83dd4c83afaa677eba88f1a6.png#pic_center" width="450">

**实现**：`from collections import deque`<br>
**操作**：
1. 创建空队列：`queue = deque()`
2. 入队：`queue.append(元素)`
3. 出队：`queue.popleft()`
4. 查看队首 / 队尾元素：`queue[0]` / `queue[-1]`
5. 判断是否为空：`not queue`
6. 长度：`len(queue)`

## 链表 Linked List
**概念**：链表是一种 线性数据结构，由若干节点（Node）组成。每个节点包含：
- 数据域（data）：存储数据
- 指针域（next）：指向下一个节点

**与数组的区别**：
- 数组内存连续，索引访问快 O(1)，但插入删除慢 O(n)
- 链表内存不连续，插入删除快 O(1)，但查找访问慢 O(n)

**单链表**：
```python
# 节点定义
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None

# 链表定义
class LinkedList:
    def __init__(self):
        self.head = None

    # 头插法
    def insert_head(self, val):
        node = Node(val)
        node.next = self.head
        self.head = node

    # 尾插法
    def insert_tail(self, val):
        node = Node(val)
        if not self.head:
            self.head = node
            return
        cur = self.head
        while cur.next:
            cur = cur.next
        cur.next = node

    # 遍历链表
    def traverse(self):
        cur = self.head
        while cur:
            print(cur.val, end=" -> ")
            cur = cur.next
        print("None")

    # 删除节点
    def delete(self, val):
        if not self.head:
            return
        if self.head.val == val:
            self.head = self.head.next
            return
        cur = self.head
        while cur.next and cur.next.val != val:
            cur = cur.next
        if cur.next:
            cur.next = cur.next.next

    # 反转链表
    def reverse(self):
        prev = None
        cur = self.head
        while cur:
            nxt = cur.next       # 暂存下一个节点
            cur.next = prev      # 反转指针
            prev = cur           # prev 前进
            cur = nxt            # cur 前进
        self.head = prev         # 更新头节点

# 创建链表
ll = LinkedList()
ll.insert_head(3)   # 链表: 3 -> None
ll.insert_head(2)   # 链表: 2 -> 3 -> None
ll.insert_head(1)   # 链表: 1 -> 2 -> 3 -> None
ll.traverse()

ll.insert_tail(4)   # 链表: 1 -> 2 -> 3 -> 4 -> None
ll.traverse()

ll.delete(2)        # 链表: 1 -> 3 -> 4 -> None
ll.traverse()

ll.reverse()        # 链表: 4 -> 3 -> 1 -> None
ll.traverse()
```


## 堆 Heap
**特点**：堆是一种特殊的完全二叉树结构，常用于优先队列，又分为
- 最小堆 (min-heap)：根节点最小
- 最大堆 (max-heap)：根节点最大

**实现**：`import heapq`<br>
**操作**：
1. 创建最小堆：
    ```python
    heap = [3, 1, 5] 
    # 将列表转为堆，默认最小堆
    # 空堆 + heappush 插入 → 不需要 heapify
    heapq.heapify(heap) # heap = [1, 3, 5]
    ```
2. 插入元素：`heapq.heappush(heap, 元素)`
3. 弹出最小元素：`x = heapq.heappop(heap)`
4. 查看最小元素：`heap[0]`

**最大堆实现方法**：
```python
# Python 没有直接的最大堆，可以通过取负数实现
max_heap = [] 
heapq.heappush(max_heap, -3) 
heapq.heappush(max_heap, -1) 
heapq.heappush(max_heap, -5)
val = -heapq.heappop(max_heap) # val = 5
```
