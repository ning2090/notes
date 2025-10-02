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

## 树 Tree
### 二叉树基本结构定义
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

```
### 二叉树的遍历方式
1. 深度优先遍历（DFS）
    - 前序遍历（Preorder）：根 → 左 → 右
        ```python
        def preorder(root):
            if not root:
                return []
            return [root.val] + preorder(root.left) + preorder(root.right)
        ```
    - 中序遍历（Inorder）：左 → 根 → 右 （BST 中序遍历得到升序序列）
        ```python
        def inorder(root):
            stack, res = [], []
            cur = root
            while cur or stack:
                while cur:
                    stack.append(cur)
                    cur = cur.left
                cur = stack.pop()
                res.append(cur.val)
                cur = cur.right
            return res
        ```
    - 后序遍历（Postorder）：左 → 右 → 根
        ```python
        from collections import deque

        def level_order(root):
            if not root:
                return []
            q = deque([root])
            res = []
            while q:
                node = q.popleft()
                res.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            return res
        ```
    - 递归实现最简单，也可用栈
2. 广度优先遍历（BFS）
    - 层序遍历（Level Order）：一层一层地访问（常用队列 collections.deque）
        ```python
        from collections import deque

        def level_order(root):
            if not root:
                return []
            res, queue = [], deque([root])
            while queue:
                level = []
                for _ in range(len(queue)):
                    node = queue.popleft()
                    level.append(node.val)
                    if node.left:
                        queue.append(node.left)
                    if node.right:
                        queue.append(node.right)
                res.append(level)
            return res
        ```
### 最大深度
```python
def max_depth(root):
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))
```
### 搜索节点
```python
def search_bst(root, val):
    if not root or root.val == val:
        return root
    if val < root.val:
        return search_bst(root.left, val)
    else:
        return search_bst(root.right, val)
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

## 哈希表 Hash Table
**定义**：哈希表是一种通过 哈希函数 (Hash Function) 将 键（Key） 映射到 值（Value） 的数据结构<br>
**常见应用**：
1. 统计频率
    ```python
    from collections import Counter

    nums = [1, 1, 2, 3, 3, 3]
    cnt = Counter(nums)  # {1:2, 2:1, 3:3}
    print(cnt[3])  # 3
    ```
2. defaultdict：和普通字典的区别是，访问不存在的键时，不会报错，而是自动创建一个默认值，默认值类型可以是int、list、set、str
    ```python
    d = defaultdict(list)
    pairs = [("a", 1), ("a", 2), ("b", 3)]

    for k, v in pairs:
        d[k].append(v)

    print(d)  # defaultdict(<class 'list'>, {'a': [1, 2], 'b': [3]})
    ```

# 算法思路
## 排序
1. 冒泡排序（Bubble Sort）：逐个交换，把最大的元素“冒泡”到最后
    ```python
    def bubble_sort(nums):
        n = len(nums)
        for i in range(n):
            for j in range(0, n - i - 1):  # 每次比较到 n-i-1
                if nums[j] > nums[j + 1]:
                    nums[j], nums[j + 1] = nums[j + 1], nums[j]
        return nums
    ```
2. 选择排序（Selection Sort）：每次选择最小的元素放到前面
    ```python
    def selection_sort(nums):
        n = len(nums)
        for i in range(n):
            min_idx = i
            for j in range(i+1, n):
                if nums[j] < nums[min_idx]:
                    min_idx = j
            nums[i], nums[min_idx] = nums[min_idx], nums[i]
        return nums
    ```
3. 插入排序（Insertion Sort）：逐个插入到合适位置
    ```python
    def insertion_sort(nums):
        for i in range(1, len(nums)):
            key = nums[i]
            j = i - 1
            while j >= 0 and nums[j] > key:
                nums[j + 1] = nums[j]
                j -= 1
            nums[j + 1] = key
        return nums
    ```
4. 归并排序（Merge Sort）：分治法：递归分成子数组再合并
    ```python
    def merge_sort(nums):
        if len(nums) <= 1:
            return nums
        mid = len(nums) // 2
        left = merge_sort(nums[:mid])
        right = merge_sort(nums[mid:])
        return merge(left, right)

    def merge(left, right):
        res, i, j = [], 0, 0
        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                res.append(left[i]); i += 1
            else:
                res.append(right[j]); j += 1
        res.extend(left[i:])
        res.extend(right[j:])
        return res
    ```
5. 快速排序（Quick Sort）：选一个基准，把小的放左边，大的放右边
    ```python
    def quick_sort(nums):
        if len(nums) <= 1:
            return nums
        pivot = nums[len(nums)//2]
        left = [x for x in nums if x < pivot]
        mid = [x for x in nums if x == pivot]
        right = [x for x in nums if x > pivot]
        return quick_sort(left) + mid + quick_sort(right)
    ```
6. 堆排序（Heap Sort）：利用堆结构不断取最大/最小值
    ```python
    import heapq

    def heap_sort(nums):
        heapq.heapify(nums)   # 小根堆
        res = [heapq.heappop(nums) for _ in range(len(nums))]
        return res
    ```

