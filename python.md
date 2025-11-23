# 输入输出
输入：`input(提示信息)` 获取到的是字符串类型<br>
输出：`print()` 默认会在末尾输出一个换行符，通过`print(..., end="")`可以不换行

# 数据类型
## Number
- int
- float
- complex 复数
- bool：true本质是数字1，false是0

## 序列
**概念**：内容连续、有序，可使用下标索引的一类数据容器。包括列表、元组、字符串<br>
**基本语法**：
- 切片 (从一个序列中，取出一个子序列)：`新序列 = 序列[起始下标:结束下标:步长]` 步长为负数表示反向取，同时起始下标和结束下标也要反向标记

### String 字符串
**特点**：只能存储字符串，无法修改<br>
**基本语法**：
- 取值：`字符串[下标索引]`
- 查找某字符的第一个匹配项的下标：`字符串.index(字符串)`
- 拼接：`+`
- 字符串的替换：`新字符串 = 字符串.replace(字符串1, 字符串2)` 不是修改本身，而是得到新字符串
- 分割：`新列表 = 字符串.split(分隔符字符串)` 按照分隔符字符串，将字符串划分为多个字符串，并存入列表对象中，字符串本身不变
- 去除前后 空格/指定字符串：`字符串.strip()` `字符串.strip(字符串)` 传入"12"就是"1"和"2"都会移除，按照单个字符
- 统计某字符在字符串内的数量：`字符串.count(字符串)`
- 统计字符数量：`len(字符串)`
- 反转：`新字符串 = 字符串[::-1]`
- 大写小写转换：`字符串.upper()` `字符串.lower()`
- 遍历
    - for循环
        ```python
        for 临时变量 in 字符串:
            ...
        ```    
    - while循环
        ```python
        index = 0
        while index < len(字符串):
            字符 = 字符串[index]
            ...
            index += 1
        ```

#### 字符串格式化
- 百分号（%）格式化
    ```python
    name = "wu"
    message = "hi %s" % name
    ```
    - `%s` 字符串占位
    - `%d` 整数占位
    - `%f` 浮点数占位
- `f"内容{变量}"`
    ```python
    print(f"我叫{name}，今年{age}岁")
    print(f"{pi:.2f}")
    ```
- `"{}".format(值)` 
    ```python
    print("我叫{}，今年{}岁".format(name, age))
    print("圆周率约为：{:.2f}".format(3.1415926))
    ```
*注意：多个变量占位变量要用括号括起来，并按照占位顺序填入

##### 精度控制
- m 控制数字宽度，设置得到宽度小于数字自身不生效，小数点和小数部分也算入宽度计算
- .n 控制小数点精度，会四舍五入

#### 字符串比较
按位比较ASCII码值，也就是一位位进行对比，只要有一位大，那么整体就大

#### 字符串判断类型
- 纯数字：`字符串.isdigit()`
- 纯字母：`字符串.isalpha()`
- 字母/数字：`字符串.isalnum()`
- 大写：`字符串.isupper()`
- 小写：`字符串.islower()`

### List 列表
**概念**：有序的可变序列<br>
**特点**：可以为不同数据类型，支持嵌套，允许重复数据，可以修改数据，有序存储 (有下标索引)<br>
**基本语法**：
- 定义
    ```python
    变量名 = [元素1, 元素2, ...]
    变量名 = list()
    ```
- 取值：`列表[下标索引]`
- 查找某元素第一个匹配项的下标：`列表.index(元素)`
- 统计元素数量：`len(列表)`
- 修改：`列表[下标索引] = 值`
- 指定位置插入元素：`列表.insert(下标, 元素)`
- 尾部追加元素：`列表.append(元素)`
- 尾部追加其他数据容器：`列表.extend(元素)` 将其他数据容器的内容取出，依次追加到列表尾部
    ```python
    my_list = [1, 2, 3]
    my_list.extend([4, 5, 6])
    print(my_list) # [1, 2, 3, 4, 5, 6]
    ```
- 删除：`del 列表[下标索引]` 或 `列表.pop(下标索引)` 还能使用pop方法的返回值得到删除的元素
- 删除某元素在列表中的第一个匹配项：`列表.remove(元素)`
- 清空列表：`列表.clear()`
- 统计某元素在列表内的数量：`列表.count(元素)`
- 反转：`列表.reverse()`
- 遍历
    - for循环
        ```python
        for 临时变量 in 列表:
            ...
        ```    
    - while循环
        ```python
        index = 0
        while index < len(列表):
            元素 = 列表[index]
            ...
            index += 1
        ```

### Tuple 元组
**概念**：有序的不可变序列<br>
**特点**：可以为多个、不同类型的元素，支持嵌套，但定义完成后不可修改<br>
**基本语法**：
- 定义
    ```python
    # 注意定义单个元素的元组，需要写成：变量名 = (元素1, )
    变量名 = (元素1, 元素2, ...)
    变量名 = tuple()
    ```
- 取值：`元组[下标索引]`
- 查找某元素第一个匹配项的下标：`元组.index(元素)`
- 统计元素数量：`len(元组)`
- 统计某元素在元组内的数量：`元组.count(元素)`
- 遍历
    - for循环
        ```python
        for 临时变量 in 元组:
            ...
        ```    
    - while循环
        ```python
        index = 0
        while index < len(元组):
            元素 = 元组[index]
            ...
            index += 1
        ```

## Set 集合
**概念**：无序 (不支持下标索引) 不重复集合<br>
**基本语法**：
- 定义
    ```python
    变量名 = {元素1, 元素2, ...}
    变量名 = set()
    ```
- 添加元素：`集合.add(元素)` 修改集合本身
- 移除元素：`集合.remove(元素)` 修改集合本身
- 随机取出元素：`集合.pop()` 会得到一个元素的结果，同时修改集合本身，该元素被移除
- 清空集合：`集合.clear()`
- 取出2个集合的差集：`新集合 = 集合1.difference(集合2)` 取出集合1有而集合2没有的，集合1和集合2不变
- 消除2个集合的差集：`集合1.difference_update(集合2)` 在集合1中删除和集合2相同的元素，集合1被修改，集合2不变
- 合并集合：`新集合 = 集合1.union(集合2)` 集合1和集合2不变
- 统计元素数量：`len(集合)`
- 遍历：for循环
    ```python
    for 临时变量 in 集合:
        ...
    ``` 

## Dictionary 字典
**概念**：无序key-value集合，不允许重复key (定义重复key时，后面的会覆盖前面的)<br>
**基本语法**：
- 定义
    ```python
    变量名 = {key1: value1, key2: value2, ...}
    变量名 = dict()
    ```
- 取value：`字典[key]`
- 添加/更新 元素：`字典[key] = value`
- 删除元素：`字典.pop(key)`
- 清空字典：`字典.clear()`
- 获取全部key：`字典.keys()`
- 获取全部value：`字典.values()`
- 统计元素数量：`len(字典)`
- 遍历：for循环
    ```python
    for key in 字典:
        # value为 字典[key]
        ...
    ``` 
    ```python
    for k, v in 字典.items():
        print(f"key: {k}, value: {v}")
    ```

# 验证类型：`type()`

# 数据类型转换
- int()
- float()
- str()

# 常用运算符
| 分类        | 运算符      | 含义          | 示例                 | 结果             |
| --------- | -------- | ----------- | ------------------ | -------------- |
| **算术运算符** | `+` | 加法  | `3 + 2`  | `5`  | 
|           | `-` | 减法| `5 - 2` | `3`|
|           | `*` | 乘法   | `3 * 2` | `6` |
|           | `/`| 除法（结果为浮点数） | `5 / 2` | `2.5`|
|           | `//`  | 整除（向下取整）| `5 // 2`  | `2` |
|           | `%`| 取余| `5 % 2` | `1` |
|           | `**` | 幂运算 | `2 ** 3`  | `8` | 
| **比较运算符** | `==`  | 等于 | `3 == 3`| `True`  |
|           | `!=`| 不等于| `3 != 2` | `True` |
|           | `>`| 大于  | `5 > 2` | `True` |
|           | `<` | 小于  | `2 < 5` | `True`| 
|           | `>=` | 大于等于 | `5 >= 5`| `True`  |
|           | `<=`| 小于等于| `3 <= 4` | `True`|
| **逻辑运算符** | `and` | 逻辑与| `True and False`| `False`|
|           | `or`| 逻辑或| `True or False` | `True` |
|           | `not`| 逻辑非 | `not True`| `False` |
| **位运算符**  | `&` | 按位与<br>两个数的对应二进制位都为 1时结果为 1 | `5 & 3`  | `1` |
|           | `  | 按位或  | `5  | 3` | `7` |
|           | `^` | 按位异或<br>相同为 0，不同为 1 | `5 ^ 3` | `6` |
|           | `~` | 按位取反<br>等价于 -(x + 1) | `~5`    | `-6` |
|           | `<<`| 左移  | `2 << 1`  | `4` |
|           | `>>` | 右移 | `4 >> 1`  | `2` |
| **赋值运算符** | `=` | 赋值  | `x = 5`| `x 为 5` |
|           | `+=` | 加后赋值  | `x += 2`    | `x = x + 2` |
|           | `-=`  | 减后赋值 | `x -= 2` | `x = x - 2`|
|           | `*=`| 乘后赋值  | `x *= 2`| `x = x * 2` |
|           | `/=`| 除后赋值 | `x /= 2` | `x = x / 2` |
|           | `//=` | 整除后赋值| `x //= 2`| `x = x // 2` |
|           | `%=` | 取余后赋值 | `x %= 2` | `x = x % 2` |
|           | `**=` | 幂后赋值 | `x **= 3` | `x = x ** 3` |
| **成员运算符** | `in`| 元素是否在序列中| `'a' in 'cat'` | `True`  |
|           | `not in` | 元素不在序列中| `'x' not in 'cat'` | `True`   |
| **身份运算符** | `is` | 判断是否是同一个对象  | `a is b` | `True / False`|
|           | `is not`| 判断是否不是同一个对象| `a is not b` | `True / False`|


# 数据容器通用操作
1. 内置函数:
    | 函数      | 功能              |
    | ------- | --------------- |
    | `max()` | 最大值       |
    | `min()` | 最小值         |
    | `sum()` | 求和      |
    | `abs()` | 绝对值         |
    | `round(x, ndigits=0)` | 四舍五入，可指定小数位数   |
    | `pow(x, y)` | 幂运算（等价于 x**y）         |
2. 容器转换：`str(容器)` `list(容器)` `tuple(容器)` `set(容器)`
3. 排序：
    - `新列表 = sorted(容器, [reverse=True])` 加上reverse=True会降序排序
    - `原列表.sort()`
4. 获取索引以及值
    ```python
    for index, item in enumerate(iterable, start=0):
        ...
    ```
5. 映射处理序列：
    ```python
    nums = [1, 2, 3]
    result = map(str, nums)         # 把每个数字转成字符串
    print(list(result))             # ['1', '2', '3']
    ```
6. 过滤 filter(function, iterable)
    ```python
    nums = [1, 2, 3, 4, 5, 6]
    result = filter(lambda x: x % 2 == 0, nums)
    print(list(result))  # [2, 4, 6]
    ```
7. 字符串变成表达式并求值：`计算结果 = eval(str)`
8. 进制转换：
    - `bin(x)` 十进制→二进制（前缀 `0b`）
    - `format(x, 'b')` 十进制→二进制，无前缀    
    - `oct(x)` 十进制→八进制（前缀 `0o`）
    - `format(x, 'o')` 十进制→八进制，无前缀
    - `hex(x)` 十进制→十六进制（前缀 `0x`）
    - `format(x, 'x')` 十进制→十六进制（小写），无前缀
    - `format(x, 'X')` 十进制→十六进制（大写），无前缀
    - `int(s, base)` 字符串s → 十进制（`base` 可取 2/8/16/任意进制）

# 其他操作
1. 将一个字符串列表中的元素拼接成一个字符串，中间用指定的字符连接
    ```python
    words = ['I', 'love', 'Python']
    result = ' '.join(words)
    print(result) # 输出：I love Python
    ```
2. 字符与Unicode编码 (ASCII 是早期仅支持英文的编码标准，
Unicode 是更大的国际标准，支持全球所有文字，Unicode 的前 128 个字符与 ASCII 一致（编号相同）) 的转换：ord()只能传入一个字符
    | 函数      | 功能              | 示例              |
    | ------- | --------------- | --------------- |
    | `ord()` | 字符 → Unicode 编码 | `ord('A') → 65` |
    | `chr()` | 编码 → 字符         | `chr(97) → 'a'` |
3. 正无穷：`float('inf')` 负无穷：`float('-inf')`

# 常用标准库
1. math模块：先导入 (import math 或 from math import 方法名) 后使用
    | 方法              | 说明                 | 示例                      |
    | --------------- | ------------------ | ----------------------- |
    | `math.ceil(x)`  | 向上取整 | `math.ceil(3.2)` → 4    |
    | `math.floor(x)` | 向下取整 | `math.floor(3.8)` → 3   |
    | `math.trunc(x)` | 截断小数部分（只保留整数部分）    | `math.trunc(-3.7)` → -3 |
    | `math.sqrt(x)` | 平方根，相当于x**0.5    | `math.sqrt(9)` → 3.0 |
2. collections模块
    - defaultdict带默认值的字典，避免 KeyError `d = defaultdict(list)`
        ```python
        from collections import defaultdict
        d = defaultdict(list)
        ```
    - deque双端队列
        ```python
        from collections import deque
        dq = deque([1, 2, 3])
        dq.appendleft(0)
        dq.popleft(0)
        ```
    - Counter统计频率：用来统计很多 可迭代对象 (iterable) 中元素出现的频率
        ```python
        from collections import Counter

        # 字符串
        s = "hello"
        print(Counter(s)) # Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})

        # 字典
        d = {"a": 10, "b": 20, "c": 30, "a": 10}
        # 值的频率
        print(Counter(d.values())) # Counter({10: 2, 20: 1, 30: 1})
        ```
3. heapq模块
    ```python
    import heapq

    nums = [5, 1, 3, 2, 4]
    # 最小堆
    heapq.heapify(nums) # [1, 2, 3, 5, 4] （最小值在堆顶，其它元素不一定完全有序）
    heapq.heappush(nums, 0) # [0, 1, 2, 3, 5, 4]
    min_val = heapq.heappop(nums) # min_val = 0

    # 最大堆，可以通过取负数实现
    max_heap = [] 
    heapq.heappush(max_heap, -3) 
    heapq.heappush(max_heap, -1) 
    heapq.heappush(max_heap, -5)
    val = -heapq.heappop(max_heap) # val = 5
    ```
4. itertools模块
    - permutations生成一个序列的所有排列（顺序不同算不同排列）
        ```python
        from itertools import permutations

        data = [1, 2, 3]
        perm_all = list(permutations(data))
        print(perm_all) # [(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)]
        ```
    - combinations生成一个序列的组合（顺序不同算同一个组合）
        ```python
        from itertools import combinations

        data = [1, 2, 3]

        # 生成长度为2的组合
        comb_2 = list(combinations(data, 2))
        print(comb_2)
        # 输出: [(1, 2), (1, 3), (2, 3)]

        # 生成所有组合
        comb = [list(c) for r in range(1, len(data)+1) for c in combinations(data, r)]
        print(comb) # [[1], [2], [3], [1, 2], [1, 3], [2, 3], [1, 2, 3]]
        ```
5. functools模块
    - reduce依次累计计算
        ```python
        from functools import reduce
        nums = [1, 2, 3, 4]
        res = reduce(lambda x, y: x + y, nums)
        print(res)  # 输出 10
        ```
6. random模块
    ```python
    import random

    # 生成 a ≤ N ≤ b 随机整数 random.randint(a, b) 
    random.randint(1, 10)

    # 生成 [0.0, 1.0) 之间随机浮点数 random.random() 
    random.random()

    # 生成 [a, b] 间的随机浮点数 random.uniform(a, b)
    random.uniform(1.5, 3.5)

    # 从序列中随机选取一个元素 random.choice(seq)
    random.choice([1,2,3])
    random.choice("abc")

    # 从序列中随机选取多个元素（可重复） random.choices(seq, k=n)
    random.choices([1, 2, 3], k=5)

    # 从序列中随机选取多个元素（不重复） random.sample(seq, k=n)
    random.sample([1,2,3,4], k=2)

    # 打乱列表顺序（修改原列表）
    lst = [1,2,3,4]
    random.shuffle(lst)
    ```

# 流程控制语句
## if语句
```python
if 条件1：
    ...
elif 条件2：
    ...
else:
    ...
```

## while循环
```python
while 条件：
    ...
```

## for循环
```python
for 临时变量 in 待处理数据集：
    ...
```

### range语句
`range(start, stop, step)` start默认为0；stop默认不包含该值；step默认为1，可以是负数

## continue
**概念**：中断本次循环，直接进入下一次循环。只能作用在所在的循环上，无法对上层循环起作用

## break
**概念**：直接结束循环。只能作用在所在的循环上，无法对上层循环起作用

# 函数
**定义**：
```python
def 函数名(形参):
    """
    函数说明
    :param x: 形参x的说明
    :return: 返回值的说明
    """
    函数体
    return 返回值
```

**调用**：`函数名(实参)`

*注意：
1. 参数和返回值不需要可省略
2. 必须先定义后使用
3. 在return后的代码不会执行
4. 不使用return语句即返回None
5. 不定长参数：形参若是`*args`，所有参数都会被args变量收集，是元组类型；形参若是`**kwargs`，所有键值对参数都会被kwargs变量收集，是字典类型

## 全局变量global
```python
num = 1

def test():
    global num
    num = 2
    print(num)

test()
```

## lambda匿名函数
```python
lambda 传入参数: 函数体（一行代码）
```
*注意：无名称的匿名函数，只可临时使用一次

# 文件的读取
## open(name, mode, encoding)读取文件
**概念**：打开或创建文件。name是文件名也可是具体路径。mode常用的三种访问模式有`r`只读方式，文件指针放在文件开头；`w`写入，若该文件已存在则原有内容删除从头开始编辑，若不存在创建新文件；`a`追加，若该文件已存在则新内容写入到已有内容之后，若不存在创建新文件
```python
f = open('python.txt','r',encoding='UTF-8')
```
*注意：f是open函数的文件对象，拥有属性和方法

**方法**：
- `文件对象.read(num)`：num是读取的数据长度，单位字节，若没有传入num，表示读取文件中所有数据
- `文件对象.readlines()`：按照行的方式把文件内容一次性读取，返回的是一个列表，每一行数据就是一个元素
- `文件对象.readline()`：一次读取一行内容
- for循环读取文件行
    ```python
    for line in open('python.txt','r'):
        print(line)
    ```
- `with open() as f`：在操作后自动close文件
    ```python
    with open('python.txt','r') as f:
        f.readlines()
    ```

## write()文件写入
**概念**：调用write内容并未真正写入文件，会积攒在程序内存中，称为缓冲区，当调用flush时才会真正写入，这样避免频繁操作硬盘导致效率下降
```python
f = open('python.txt','w')
f.write('hello')
# 刷新
f.flush()
f.close()
```

## close() 关闭文件，内置flush功能

# 捕获异常
- 捕获常规异常
    ```python
    try:
        可能发生错误的代码
    except [异常 as 别名]:
        如果出现异常执行的代码
    [else:]
        没有异常时执行的代码
    [finally:]
        无论是否有异常都执行的代码
    ```
- 捕获多个异常
    ```python
    try:
        print(1/0)
    except (NameError, ZeroDivisionError):
        print('变量未定义 或 除以0异常错误')
    ```
    *注意：捕获Exception就是捕获所有异常

**异常特点**：传递性

# 模块导入
```python
[from 模块名] import [模块|类|变量|函数|*] [as 别名]
```
*注意：导入不同模块的同名功能，调用到的是后面导入的模块功能

## 自定义模块自测
```python
def test(a,b):
    print(a+b)

# 只在当前文件内调用该函数，其他导入该文件的文件内不会执行该函数
if __name__ == '__main__':
    test(1,2)
```

## __all__
**概念**：当模块文件内有__all__变量，当使用from xxx import *时，智能导入这个列表中的元素
```python
__all__ = ['test_A']

def test_A():
    print('testA')

def test_B():
    print('testB')
```

# Json数据转化
```python
import json
data = [{"name":"wu","age":18},{"name":"yu","age":18}]
# 把python数据转化为json数据。默认所有非 ASCII 字符会转义成 \uXXXX，如果数据中有中文添加ensure_ascii=False，输出正常的中文
data = json.dumps(data, ensure_ascii=False)
# 把json数据转化为python数据
data = json.loads(data)
```

# class类
```python
class Student:
    name = None
    age = None
    def say(self, msg):
        print(f"hi, {self.name},{msg}")

stu_1 = Student()
stu_1.name = 'wu'
stu_1.age = 18
stu_1.say("hello")
```

## 类内置方法——魔术方法
1. __init__构造方法：使用构造方法对成员变量进行赋值，内部自动调用这些方法，就不用像上面的代码一样一个个进行赋值了
    ```python
    class Student:
        def __init__(self, name, age):
            self.name = name
            self.age = age

    stu_1 = Student("wu", 18)
    ```
2. __str__字符串方法：原本类对象转换成字符串时，会输出内存地址，使用该方法可以控制类转换成字符串
    ```python
    class Student:
        def __init__(self, name, age):
            self.name = name
            self.age = age
        
        def __str__(self):
            return f"hi,{self.name}"

    stu_1 = Student("wu", 18)
    print(stu_1) # hi,wu
    print(str(stu_1)) # hi,wu
    ```
3. __lt__小于符号 __gt__大于符号比较
    ```python
    class Student:
        def __init__(self, name, age):
            self.name = name
            self.age = age
        
        def __lt__(self, other):
            return self.age < other.age

    stu_1 = Student("wu", 18)
    stu_2 = Student("yu", 19)
    print(stu_1 < stu_2) # True
    ```
4. __le__小于等于符号 __ge__大于等于符号比较
5. __eq__符号==比较
6. __ne__符号!=比较

## 私有成员
**概念**：在类中提供仅供内部使用的属性和方法，类对象无法使用
```python
class Student:
    name = None
    age = None
    # 私有成员变量
    __telephone = None
    def say(self, msg):
        print(f"hi, {self.name},{msg}")
    # 私有成员方法
    def __say_telephone(self):
        print(f"tel：{self.__telephone}")

stu_1 = Student()
```

## 继承
1. 单继承
    ```python
    class Phone:
        producer = None
        def call_by_4g(self):
            print("4g通话")

    class Phone2025(Phone):
        face_id = True
        def call_by_5g(self):
            print("5g通话")
    ```
2. 多继承：若父类有同名属性或方法，先继承的优先级高于后继承
    ```python
    class 类名(父类1, 父类2, ...):
        类内容体
    ```

### pass关键字
**概念**：是一个占位语句，用于代码块中暂时不写任何内容时保持语法正确

### super()调用父类成员
**概念**：用于在子类中调用父类的方法或属性
```python
class Phone:
    producer = "ITCAST"
    def call_by_4g(self):
        print("4g通话")

class MyPhone(Phone):
    # 复写
    producer = "ITCAST"
    def call_by_4g(self):
        # 方式1调用父类成员
        print(f"父类品牌：{Phone.producer}")
        phone.call_by_4g(self)

        # 方式2调用父类成员
        print(f"父类品牌：{super().producer}")
        super().call_by_4g(self)
```

## 多态
```python
# 包含抽象方法（指的是没有具体实现的方法pass）的类称为抽象类，方便子类做具体实现
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        print("汪汪汪")

class Cat(Animal):
    def speak(self):
        print("喵喵喵")

def make_noise(animal:Animal):
    animal.speak()

dog = Dog()
cat = Cat()
make_noise(dog) # 汪汪汪
make_noise(cat) # 喵喵喵
```

# 类型注解
```python
var_1:bool = True
my_list: list[int] = [1,2,3]
def 函数/方法名(形参:类型) -> 返回值类型:
    pass
```

## Union类型
**概念**：先 `from typing import Union`，再 `Union[类型, ...]`定义联合类型注解

# 闭包
```python
def outer(logo):
    def inner(msg):
        print(f"<{logo}>{msg}<{logo}>")
    return inner

fn1 = outer('hi')
fn1('wjn') # <hi>wjn<hi>
fn1('ysy') # <hi>ysy<hi>
```

## nonlocal关键字
**概念**：修改外部函数的值
```python
def outer(num1):
    def inner(num2):
        nonlocal num1
        num1 += num2
        print(num1)
    return inner

fn1 = outer(10)
fn1(10) # 20
fn1(10) # 30
```

## 装饰器
**概念**：创建一个闭包函数，在闭包函数内调用目标函数，可以达到不改动目标函数的同时，增加额外的功能
```python
def my_decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")
    return wrapper

@my_decorator
def say_hello():
    print("Hello")

say_hello()
```

# 进程、线程
**概念**：操作系统中可以运行多个进程，即多任务运行，进程之间是内存隔离的。一个进程内可以运行多个线程，即多线程运行，多个线程之间是共享这个进程所拥有的内存空间的

## python多线程——threading
```python
import threading

# group：用于未来扩展，一般填None。target：线程要执行的目标函数。name：线程的名称，默认会自动生成。args：以元组方式给执行任务传参。kwargs：以字典方式给执行任务传参。
thread_obj = threading.Thread([group[,target[,name[,args[,kwargs]]]]])

thread_obj.start()
```

# Socket
**概念**：负责进程之间的网络数据传输

## Python Socket 服务端编程
```python
import socket

# 1. 创建socket对象
server_socket = socket.socket()

# 2. 绑定 IP 和端口号
server_socket.bind(('127.0.0.1', 8888))

# 3. 开始监听，最多允许 5 个连接等待
server_socket.listen(5)

# 4. 等待客户端连接
client_socket, addr = server_socket.accept()
print(f"客户端已连接，地址：{addr}")

# 5. 接收客户端数据（最多 1024 字节）
data = client_socket.recv(1024)
print("收到客户端消息：", data.decode())

# 6. 回复客户端
client_socket.send("你好，客户端！".encode())

# 7. 关闭连接
client_socket.close()
server_socket.close()
```

## Python Socket 客户端编程
```python
import socket

# 1. 创建 socket 对象
client_socket = socket.socket()

# 2. 连接服务器（IP 地址和端口要与服务端一致）
client_socket.connect(('127.0.0.1', 8888))

# 3. 发送数据给服务端
client_socket.send("你好，服务端！".encode())

# 4. 接收服务端回复的数据，1024是缓冲区大小，一般1024即可
data = client_socket.recv(1024)
print("收到服务端消息：", data.decode())

# 5. 关闭连接
client_socket.close()
```

# 正则表达式
**基础方法**：
1. `re.match(匹配规则, 被匹配的字符串)`：从字符串开头匹配，只匹配开头，成功返回match对象，失败返回None
    ```python
    import re

    s = "hello world"
    result = re.match(r'hello', s)  # 开头匹配"hello"
    print(result)  # <re.Match object; span=(0, 5), match='hello'>
    print(result.group())  # hello
    ```
2. `re.search(匹配规则, 被匹配的字符串)`：在整个字符串中搜索第一个匹配，返回match对象，失败返回None
    ```python
    import re

    s = "say hello world"
    # 这里的r表示字符串中转义字符无效，就是普通字符的意思
    result = re.search(r'hello', s)  # 查找第一个"hello"
    print(result)  # <re.Match object; span=(4, 9), match='hello'>
    print(result.group())  # hello
    ```
3. `re.findall(匹配规则, 被匹配的字符串)`：返回所有匹配的结果，列表形式，没有返回空列表[]
    ```python
    import re

    s = "hello world, hello python"
    result = re.findall(r'hello', s)  # 查找所有"hello"
    print(result)  # ['hello', 'hello']
    ```

## 元字符匹配
**单字符匹配**：
| 表达式  | 含义                     | 
| ---- | ---------------------- | 
| `.`  | 匹配**除换行符外**的任意单个字符     | 
| `\d` | 匹配**数字**（0-9）          | 
| `\D` | 匹配**非数字**              | 
| `\w` | 匹配**字母、数字、下划线**        | 
| `\W` | 匹配**非字母、数字、下划线**       | 
| `\s` | 匹配**空白字符**（空格、制表符、换行符） | 
| `\S` | 匹配**非空白字符**            | 

**数量匹配**：
| 表达式     | 含义                |
| ------- | ----------------- |
| `*`     | 重复**0次或多次**       |
| `+`     | 重复**1次或多次**       |
| `?`     | 重复**0次或1次**       |
| `{n}`   | 重复**n次**          |
| `{n,}`  | 重复**至少n次**        |
| `{n,m}` | 重复**n到m次（包含n和m）** |

**边界匹配**：
| 表达式  | 含义                      |
| ---- | ----------------------- |
| `^`  | 匹配**字符串的开头**            |
| `$`  | 匹配**字符串的结尾**            |
| `\A` | 匹配**字符串开始位置**（不受多行模式影响） |
| `\Z` | 匹配**字符串结束位置**（不受多行模式影响） |
| `\b` | 匹配**单词边界**              |
| `\B` | 匹配**非单词边界**             |

**分组匹配**：
| 表达式             | 含义                   |
| --------------- | -------------------- |
| `()`            | 分组，提取子串，或用于数量限定符作用范围 |
| `(?:...)`       | 非捕获分组，仅分组但不捕获        |
| `(?P<name>...)` | 命名分组，分组的同时给该分组命名     |
| `(?P=name)`     | 引用命名分组               |
| `\num`          | 引用第 num 个分组（数字从1开始）  |

# 递归
**概念**：函数自己调用自己

# 内存管理机制
1. 引用计数机制：Python 通过为每个对象维护引用计数，在引用为零时立即回收内存
2. 垃圾回收机制：为了处理循环引用，Python 引入了基于分代收集的垃圾回收机制
3. 内存池机制：Python 使用内存池（如 pymalloc）来提高小对象的内存分配与释放效率


# GIL 全局解释器锁
**概念**：是 Python 解释器为保证线程安全而设置的一个锁，它限制了同一时刻只有一个线程在执行 Python 字节码