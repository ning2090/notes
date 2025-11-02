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

## 二分查找
```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1  # 没找到返回 -1
```

## 滑动窗口(双指针)
```python
# 长度最小的子数组（找到最短连续子数组，其和 ≥ target）
def min_subarray_len(target, nums):
    left = 0
    total = 0
    res = float('inf')

    for right in range(len(nums)):
        total += nums[right]

        # 当条件满足时，尝试收缩左边界
        while total >= target:
            res = min(res, right - left + 1)
            total -= nums[left]
            left += 1

    return 0 if res == float('inf') else res
```

## 贪心算法 Greedy Algorithm
**思想**：每一步都采取当前最优选择（局部最优）的算法思想，希望通过这些局部最优解，最终得到全局最优解
```python
# 区间调度问题（最多不重叠区间）。思路：每次选择“结束时间最早”的区间，留下更多空间给后续区间
def eraseOverlapIntervals(intervals):
    intervals.sort(key=lambda x: x[1])  # 按结束时间排序
    count = 0
    end = float('-inf')

    for i in intervals:
        if i[0] >= end:  # 当前区间与前一个不重叠
            end = i[1]
            count += 1

    return len(intervals) - count  # 需要移除的区间数
```

## 广度优先搜索 BFS
```python
# 最短路径
from collections import deque

def shortestPath(grid, start, end):
    m, n = len(grid), len(grid[0])
    sx, sy = start
    ex, ey = end

    # 四个方向：上、下、左、右
    directions = [(-1,0), (1,0), (0,-1), (0,1)]

    queue = deque([(sx, sy, 0)])  # (x, y, 距离)
    visited = set([(sx, sy)])

    while queue:
        x, y, dist = queue.popleft()
        
        # 到达终点
        if (x, y) == (ex, ey):
            return dist

        # 遍历四个方向
        for dx, dy in directions:
            nx, ny = x + dx, y + dy

            # 判断边界和是否可走（假设1是障碍，0是可走）
            if 0 <= nx < m and 0 <= ny < n and grid[nx][ny] == 0 and (nx, ny) not in visited:
                visited.add((nx, ny))
                queue.append((nx, ny, dist + 1))

    return -1  # 若无法到达终点
```

## 深度优先搜索 DFS
```python
def dfs(grid, x, y, visited):
    m, n = len(grid), len(grid[0])

    # 边界条件：出界 或 已访问 或 障碍（假设1是障碍，0是可走）
    if x < 0 or x >= m or y < 0 or y >= n or grid[x][y] == 1 or (x, y) in visited:
        return

    visited.add((x, y))  # 标记已访问

    # 四个方向：上、下、左、右
    directions = [(-1,0), (1,0), (0,-1), (0,1)]

    for dx, dy in directions:
        dfs(grid, x + dx, y + dy, visited)
```
案例 1：二维迷宫，打印出所有路径
```python
def allPaths(maze, start, end):
    rows, cols = len(maze), len(maze[0])
    res = []
    path = []
    visited = set()
    directions = [(1,0), (-1,0), (0,1), (0,-1)]

    def dfs(x, y):
        path.append((x, y))
        if (x, y) == end:
            res.append(path[:])
        else:
            visited.add((x, y))
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < rows and 0 <= ny < cols and maze[nx][ny] == 0 and (nx, ny) not in visited:
                    dfs(nx, ny)
            visited.remove((x, y))  # 回溯
        path.pop()

    dfs(*start) # 参数解包语法。等价于dfs(start[0], start[1]) 
    return res
```
案例 2：网格中的岛屿数量（经典 DFS 搜索连通块）
```python
def numIslands(grid):
    if not grid:
        return 0
    rows, cols = len(grid), len(grid[0])
    visited = set()

    def dfs(r, c):
        if (r < 0 or c < 0 or r >= rows or c >= cols or 
            grid[r][c] == '0' or (r, c) in visited):
            return
        visited.add((r, c))
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)

    count = 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1' and (r, c) not in visited:
                dfs(r, c)
                count += 1
    return count


grid = [
    ["1","1","0","0","0"],
    ["1","1","0","0","0"],
    ["0","0","1","0","0"],
    ["0","0","0","1","1"]
]
print(numIslands(grid))  # 输出 3
```

## 递归
**概念**：函数在定义中直接或间接调用自身
```python
# 斐波那契数列（Fibonacci）
def fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)

print(fib(6))  # 输出：8
```

## 回溯
**思想**：构建搜索树，探索所有可能解。在搜索过程中，如果发现当前路径不能得到正确解，就撤销（回溯），尝试其他可能。
```python
def backtrack(路径 path, 选择列表 options):
    if 满足结束条件:
        res.append(path的某种形式)
        return

    for option in options:
        # 做选择
        path.append(option)
        # 递归进入下一层决策
        backtrack(path, 更新后的 options)
        # 撤销选择
        path.pop()
```
案例 1：子集问题
```python
def subsets(nums):
    res = []

    def backtrack(start, path):
        res.append(path[:])  # 每一步都记录子集
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()

    backtrack(0, [])
    return res
```
案例 2：全排列问题（给定一组不重复的数字，返回所有排列）
```python
def permute(nums):
    res = []

    def backtrack(path, used):
        if len(path) == len(nums):
            res.append(path[:])
            return
        for i in range(len(nums)):
            if used[i]:
                continue
            path.append(nums[i])
            used[i] = True
            backtrack(path, used)
            path.pop()
            used[i] = False

    backtrack([], [False]*len(nums))
    return res
```

## 动态规划
案例 1：一维 DP：爬楼梯问题（每次可以爬 1 或 2 个台阶，问共有多少种方法到达顶层）
```python
def climbStairs(n):
    if n <= 2:
        return n
    dp = [0] * (n + 1)
    dp[1], dp[2] = 1, 2
    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]  # 状态转移方程
    return dp[n]
```

案例 2：二维 DP：最小路径和（从左上角到右下角的最小路径和，只能向右或向下走）
```python
def minPathSum(grid):
    m, n = len(grid), len(grid[0])
    dp = [[0]*n for _ in range(m)]
    dp[0][0] = grid[0][0]
    for i in range(1, m):
        dp[i][0] = dp[i-1][0] + grid[i][0]
    for j in range(1, n):
        dp[0][j] = dp[0][j-1] + grid[0][j]
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
    return dp[-1][-1]
```

案例 3：背包问题
```python
def knapsack(weights, values, W):
    n = len(weights)
    dp = [0] * (W + 1)
    for i in range(n):
        for j in range(W, weights[i] - 1, -1):
            dp[j] = max(dp[j], dp[j - weights[i]] + values[i])
    return dp[W]
```

## 最小生成树（MST, Minimum Spanning Tree）
常见题目：有 N 个城市和 M 条候选道路，每条道路有修建成本，问连接所有城市的最小花费
### Kruskal算法（适合稀疏图）
```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False
        self.parent[py] = px
        return True


def kruskal(n, edges):
    """
    n: 节点个数
    edges: 边列表 [ (u, v, w), ... ]，w是权值
    返回最小生成树的总权值
    """
    uf = UnionFind(n)
    mst_weight = 0
    edge_count = 0

    # 按权值从小到大排序
    edges.sort(key=lambda x: x[2])

    # 遍历边，若不成环就加入
    for u, v, w in edges:
        if uf.union(u, v):
            mst_weight += w
            edge_count += 1
            if edge_count == n - 1:  # 已生成 n-1 条边
                break

    return mst_weight
```

### Prim算法（适合稠密图）
```python
import heapq

def prim(n, graph):
    """
    n: 节点个数
    graph: 邻接表 {u: [(v, w), ...], ...}
    返回最小生成树的总权值
    """
    visited = [False] * n
    min_heap = [(0, 0)]  # (权值, 节点)
    total_weight = 0

    while min_heap:
        w, u = heapq.heappop(min_heap)
        if visited[u]:
            continue
        visited[u] = True
        total_weight += w

        for v, w2 in graph[u]:
            if not visited[v]:
                heapq.heappush(min_heap, (w2, v))

    return total_weight
```

## 其他
案例 1：获取所有子集
```python
def subsets_simple(nums):
    res = [[]]  # 初始子集为空集
    for num in nums:
        res += [curr + [num] for curr in res]  # 每个已有子集加上 num 形成新子集
    return res

print(subsets_simple([1,2,3]))
# 输出: [[], [1], [2], [1,2], [3], [1,3], [2,3], [1,2,3]]
```
