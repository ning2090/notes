# JavaScript
**概念**：是一种运行在服务端（浏览器）的编程语言，实现人机交互效果<br>
**作用**：
1. 网页特效（监听用户的一些行为让网页作出对应的反馈）
2. 表单验证（针对表单数据的合法性进行判断）
3. 数据交互（获取后台的数据，渲染到前端）
4. 服务端编程（node.js）

<img src="https://i-blog.csdnimg.cn/direct/959ded5575f54aa4baf4cf1156ece80f.png#pic_center" width="400">

## 书写位置
1. 内联
    ```html
    <body>
        <button onclick="alert('hi')">点击</button>
    </body>
    ```
2. 内部
    ```html
    <body>
        <script>
            alert('hi')
        </script>
    </body>
    ```
    *注意：script标签需要放在html文件底部，因为浏览器会按照代码在文件中的顺序加载html
3. 外部
    ```html
    <body>
        <script src="my.js"></script>
    </body>
    ```
## 输入语法
`prompt('请输入：')` 显示一个对话框，并有输入提示。用prompt获取的是字符串型

## 输出语法
1. `document.write('内容')` 向body内输出内容（若内容写的是标签，会被解析成网页元素）
2. `alert('内容')` 页面弹出警告对话框
3. `console.log('内容')` 控制台打印内容

## 变量 let
**本质**：是程序在内存中申请的一块用来存放数据的小空间<br>
**命名规则**：
- 不能用特殊含义的字符
- 只能用下划线、字母、数字、$组成，且数字不能开头
- 区分大小写

**用法**：
- 声明变量 `let 变量名` 
- 变量赋值 `age = 18` 其中18是字面量（字面量是一种表示固定值的表示法，它直接表示了值本身，而不是一个变量名或表达式）
- 变量初始化 `let name = ['w','j','n']`<br> 
*注意：let不允许多次声明一个变量

## 常量 const
**用法**：与变量类似<br>
*注意：const声明时必须要赋值，进行初始化

## 数据类型
- 基本数据类型（又叫简单类型或值类型）：变量中存储的是值本身
    - number 数字型
    - string 字符串型
    - boolean 布尔型
    - undefined 未定义型
    - null 空类型
    - 等等
- 引用数据类型（又叫复杂类型）：通过new关键字创建的对象，如Object、Array、Date等，变量中存储的是地址（引用）
    - object 对象
    - array 数组
    - function 函数
    - 等等

*注意：
1. JS是弱数据类型，只有变量赋值后才能确定该变量属于那种类型，而Java是强数据类型，例如 int a = 3，必须是整数
2. NaN代表一个计算错误，是一个不正确的或者一个未定义的数学操作所得到的结果，且是粘性的，任何对NaN的操作都会返回NaN
3. 通过单引号、双引号、反引号包裹的数据都叫字符串
4. +用来字符串的拼接
5. 只声明变量未赋值的情况，变量默认值为undefined，应用场景，可以检测变量为undefined表示值还没有传进来
6. null表示赋值了，但是内容为空，可以作为尚未创建的对象

### 检测数据类型
typeof运算符可以返回被检测的数据类型，支持以下两种语法形式：
- 作为运算符：typeof x
- 函数形式：typeof(x)

## 类型转换
### 隐式转换
**概念**：某些运算符被执行时，系统内部自动将数据类型进行转换<br>
**规则**：
1. +号两边只要有一个是字符串，都会把另外一个转成字符串
2. 除了+以外的算术运算符，都会把数据转成数字型。减法会使空字符串转换成0，例如`console.log('' - 1)`结果为数字型-2
3. +号作为正号解析可以转换成数字型，例如`console.log(+'123')`结果为数字型123
4. null经过数字转换后会变成0，例如`console.log(null + 1)`结果为数字型1
5. undefined经过数字转换后会变成NaN，例如`console.log(undefined + 1)`结果为NaN
6. `console.log(null == undefined)`结果为true，但`console.log(null === undefined)`结果为false

### 显式转换
- 转换成数字型
    - `Number(数据)` 注意若字符串里有非数字，转换结果为NaN；NaN也是number类型的数据，代表非数字
    - `parseInt(数据)` 只保留整数
    - `parseFloat(数据)` 可以保留小数
- 转换成布尔型
    - `Boolean(数据)` 其中''、0、undefined、null、false、NaN转换成布尔值后都是false，其余为true

## 运算符
- 赋值运算符
- 一元运算符、二元运算符、三元运算符
- 比较运算符
- 逻辑运算符

*注意：
1. 前置自增（++num）和后置自增（num++）单独使用没有区别，若参与运算就有区别，如下代码
    ```js
    let i = 1
    console.log(++i + 1);// 结果3。i先自加变成2后再加后面的1
    let j = 1
    console.log(j++ + 1);// 结果2。i先和1相加，运算完输出完毕后，i再自加变成2
    ```
2. 比较运算符中==是两边值是否相等，===是两边值和类型都是否相等
3. 字符串比较，比较的是字符对应的ASCII码（其中A对应65，a对应97），从左往右依次比较；NaN不等于任何值，包括它本身，所以涉及到NaN都是false；尽量不要比较小数，因为有精度问题；不同类型间的比较会发生隐式转换
4. 逻辑运算符分为&&与、||或、!非
5. 运算符优先级

    | 优先级     | 运算符     |顺序     |
    | -------- | -------- |-------- |
    | 1| 小括号 |() |
    | 2| 一元运算符 |! ++ -- |
    | 3| 算数运算符 |先* / % 后+ - |
    | 4| 关系运算符 |> >= < <= |
    | 5| 相等运算符 |== != === !== |
    | 6| 逻辑运算符 |先与后或 |
    | 7| 赋值运算符 |= |
    | 8| 逗号运算符 |, |

## 术语
| 术语     | 解释     |举例     |
| -------- | -------- |-------- |
| 关键字| 在js中有特殊意义的词汇 |let、const、function等 |
| 保留字| 目前js中没意义 |int、short、long、char等 |
| 标识（标识符）| 变量名、函数名的另一种叫法 |无 |
| 表达式| 能产生值得代码，一般配合运算符出现 |10 + 3 |
| 语句| 一段可执行得代码 |if()等 |

## 三大流程控制语句
- 顺序结构
- 分支结构
    - if分支语句
        ```js
        if(条件1){
            代码1
        }else if(条件2){
            代码2
        }else{
            代码3
        }
        ```
    - 三元运算符 `条件 ? 满足条件执行的代码 : 不满足条件执行的代码`
    - switch语句
        ```js
        // switch case一般用于等值判断，必须是===全等，不适合区间判断，需要配合break使用，否则会造成case穿透
        switch(数据){
            case 值1:
                代码1
                break
            case 值2:
                代码2
                break
            default:
                代码3
                break
        }
        ```
- 循环结构
    - while循环
        ```js
        // 循环三要素：变量起始值、终止条件、变量变化量
        // break退出整个循环；continue结束本次循环，继续下次循环
        while(循环条件){
            循环体
        }
        ```
    - for循环
        ```js
        for(变量起始值; 终止条件; 变量变化量){
            循环体
        }
        ```

## 断点调试
**步骤**：
1. 浏览器F12打开开发者工具
2. 点开sources一栏
3. 选择代码文件并在语句断点

## 数组
1. 声明语法(可以存储任意类型数据；索引或下标从0开始)
    - 方法1：`let 数组名 = [数据1, 数据2, ..., 数据n]`
    - 方法2：`let 数组名 = new Array(数据1, 数据2, ..., 数据n)`
2. 长度语法 `数组名.length`
3. 查询 `数组名[索引]`
4. 修改 `数组名[索引] = 新值`
5. 新增
    - `arr.push(元素1, ..., 元素n)` 将一个或多个元素添加到数组末尾，返回该数组的新长度
    - `arr.unshift(元素1, ..., 元素n)` 将一个或多个元素添加到数组的开头，返回该数组的新长度
6. 删除 
    - `arr.pop()` 从数组中删除最后一个元素，并返回该元素的值
    - `arr.shift()` 从数组中删除第一个元素，并返回该元素的值
    - `arr.splice(操作的下标, 删除的个数)` 指定删除，其中删除的个数可选，不写删除的个数默认删除到最后。可选删除的个数后面再加参数，则这些参数指要插入的新元素
7. 数组排序（与冒泡排序（两个两个比较，先排序完一个再看另一个）后结果相同，直接修改原数组，而不是返回一个新数组）
    ```js
    // 升序
    arr.sort((a, b) => a - b) 
    // 降序
    arr.sort((a, b) => b - a)
    ```
8. 遍历数组
    - 方法1：for循环
        ```js
        for(let i = 0; i < 数组名.length; i++){
            数组名[i]
        }
        ```
    - 方法2：forEach方法（没有返回值）索引号可选
        ```js
        const arr = ['red', 'blue']
        arr.forEach(function(element,index){
            console.log(element)
            console.log(index)
        })
        ```
    - 方法3：map方法（也称为映射，有返回值）
        ```js
        const arr = ['red', 'blue']
        const newArr = arr.map(function(ele,index){
            console.log(ele) // 数组元素
            console.log(index) // 数组索引号
            return ele + '颜色'
        })
        console.log(newArr) // ['red颜色', 'blue颜色']
        ```
9. 常用方法
    - join方法：把数组中的所有元素转换成一个字符串，参数代表分隔符，''代表空字符串，表示元素间没有任何字符，参数为空则默认是逗号分割
        ```js
        const arr = ['red颜色', 'blue颜色']
        console.log(arr.join('')) // red颜色blue颜色
        ```
    - filter方法：筛选数组。创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，若没有符合条件的元素则返回空数组。index可选
        ```js
        const score = [10, 50, 3, 33]
        const re = score.filter(function(element){
            return element > 30
        })
        console.log(re)// [50, 33]
        ```
    - slice方法：截取并返回新数组。slice(start, end)从下标 start 开始，截取到（不包含）end
        ```js
        const arr = [10, 20, 30, 40, 50]
        const sliced = arr.slice(1, 4)
        console.log(sliced)  // [20, 30, 40]
        ```
    - concat方法：合并数组，返回新数组
        ```js
        const arr1 = [1, 2]
        const arr2 = [3, 4]
        console.log(arr1.concat(arr2))  // [1, 2, 3, 4]
        ```

修改原数组的方法：push()、pop()、shift()、unshift()、splice()、sort()、reverse() 等<br>
返回新数组的方法：map()、filter()、slice()、concat() 等

## 对象
**概念**：无序的数据集合
1. 声明语法（{}是对象字面量。对象由属性和方法组成）
    - 利用对象字面量创建对象：`let 对象名 = {属性名: 属性值, 方法名: 函数}`
    - 利用new Object创建对象：`let 对象名 = new Object()`
    - 利用构造函数创建对象（用于快速创建多个类似的对象）：
        ```js
        function Pig(name, age, gender){
            this.name = name
            this.age = age
            this.gender = gender
        }
        const Peppa = new Pig('佩奇', 6, '女')
        ```
        *注意：实例化构造函数时没有参数可以省略。实例化执行过程：1.创建新的空对象 2.构造函数this指向新对象 3.执行构造函数代码，修改this，添加新的属性 4.返回新对象
2. 查询 
    - 方法1：`对象名.属性名`
    - 方法2：`对象名['属性名']`
3. 修改 `对象名.属性名 = 值`
4. 新增 `对象名.新属性名 = 新值`
5. 删除 `delete 对象名.属性名`
6. 方法调用 `对象名.方法名()`
7. 遍历对象
    ```js
    for (let k in obj) {
        console.log(k) // 打印属性名，字符串
        console.log(obj[k]) // 打印属性值
    }
    ```
**内置对象—Math**：
- random方法：生成[0,1)间的随机数，例如 `Math.floor(Math.random() * (M - N + 1)) + N` 生成N-M之间的随机整数
- ceil方法：向上取整
- floor方法：向下取整
- max方法：找最大数
- min方法：找最小数
- pow方法：幂运算
- abs方法：绝对值

## 函数
1. 具名函数
    - 声明语法（这里的参数是形参）
        ```js
        function 函数名(参数1 = 0, ..., 参数n = 0){
            函数体
            return 数据
        }
        ```
    - 调用语法 `函数名(传递的参数列表)` （这里的参数是实参）
2. 匿名函数 
    - 声明语法`function(){}`
    - 调用语法
        - 函数表达式
            ```js
            let fn = function(x, y){
                console.log(x + y); 
            }
            fn(1, 2)
            ```
        - 立即执行函数
            ```js
            // 无需调用，立即执行。多个立即执行函数要用;分开，否则会报错
            // 方式1
            (function(){console.log(1)})();
            // 方式2
            (function(){console.log(1)}());
            ```

*注意：
1. 参数1 = 0是在设置形参默认值，若形参没有默认值，则默认为undefined
2. return后代码不会再被执行，所以return后数据不要换行写
3. 可以没有return，会默认返回值为undefined
4. 两个相同函数，后面的会覆盖前面的函数
5. js中，实参个数和形参个数可以不一致。若形参过多，会自动填上undefined；若实参过多，多余的实参会被忽略
6. 具名函数的调用可以写到任何位置，而匿名函数的调用必须在声明后

## 作用域
- 全局作用域：函数外部或者整个script有效。为window对象动态添加的属性默认是全局的，函数中未使用任何关键字声明的变量为全局变量。尽可能少的声明全局变量，防止全局变量被污染（全局变量）
- 局部作用域：也称函数作用域，函数内部有效（局部变量）
    - 函数作用域：函数内部声明的变量只能在函数内部被访问，外部无法直接访问。不同函数内部声明的变量无法相互访问。函数执行完毕后，函数内部的变量实际被清空了
    - 块作用域：在js中使用{}包裹的代码称为代码块，其内部声明的变量外部有可能无法被访问。let、const声明的变量会产生块作用域，而var不会产生块作用域
        ```js
        for(let t = 1; t <= 6; t++){
            console.log(t)// 正常
        }
        console.log(t)// 报错
        ```

### 变量的访问原则
- 只要是代码就至少有一个作用域
- 写在函数内部的局部作用域
- 如果函数中还有函数，那么在这个作用域中又可以诞生一个作用域
- 访问原则：在能够访问到的情况下，先局部再找全局

### 作用域链
**概念**：变量的查找机制。在函数被执行时。嵌套关系的作用域串联起来形成了作用域链。相同的作用域链中按着从小到大的规则查找变量。子作用域能访问父作用域，但父级作用域无法访问子级作用域<br>
**查找规则**：会优先查找当前函数作用域中变量，如果当前作用域查找不到则会逐级查找父级作用域直到全局作用域

## 逻辑中断
- 逻辑运算符里的短路，只存在于&&和||中
    - && 左边为false就短路，即右边不执行。两边都为真，返回最后一个真值
    - || 左边为true就短路。两边都为真，返回第一个真值

## 堆栈空间
1. 栈（操作系统）：由操作系统自动分配释放存放函数的参数值、局部变量的值等。简单数据类型会存放到栈里
2. 堆（操作系统）：存储复杂类型（对象），一般由程序员分配释放，若不释放，则由垃圾回收机制回收

<img src="https://i-blog.csdnimg.cn/direct/c90455ee3e2c438da9ef8caed91c3f48.png#pic_center" width="600">

<img src="https://i-blog.csdnimg.cn/direct/485e470979ee4fd8bc51701931860856.png#pic_center" width="600">

<img src="https://i-blog.csdnimg.cn/direct/777a6deadbb8410c94a9931534b278fe.png#pic_center" width="600">

## Web APIs
### DOM树
**概念**：将html文档以树状结构直观表现出来

<img src="https://i-blog.csdnimg.cn/direct/b0987a0bdd854b50b6270ed864cb5133.png#pic_center" width="600">

### DOM对象
**概念**：浏览器根据html标签生成的JS对象。所有的标签属性都可以在这个对象上面找到。修改这个对象的属性会自动映射到标签身上<br>
**DOM核心思想**：把网页内容当作对象来处理<br>
**document对象**：是DOM里提供的一个对象，它提供的属性和方法都用来访问和操作网页内容，网页所有内容都在document里面

### 获取DOM元素
1. 根据CSS选择器来获取DOM元素
    - `document.querySelector('css选择器')` 选择匹配的第一个元素，若没有匹配到返回null。参数包含一个或多个有效的CSS选择器字符串。能直接操作修改
    - `document.querySelectorAll('css选择器')` 选择匹配的多个元素，返回的是NodeList对象集合，得到的是一个伪数组 (伪数组长得像数组，可以用数字下标访问、length属性等，但不能直接使用数组的方法，如push、forEach等)。参数包含一个或多个有效的CSS选择器字符串。不能直接修改，需要通过遍历的方式给里面的元素做修改
2. 其他方法
    - `document.getElementById('nav')` 根据id获取一个元素
    - `document.getElementsByTagName('div')` 根据标签获取一类元素，该例子获取了页面所有div
    - `document.getElementsByClassName('w')` 根据类名获取所有元素

### 操作元素内容
1. `对象.innerText` 显示纯文本，不解析标签
2. `对象.innerHTML` 会解析标签，多标签建议使用模板字符

### 操作元素属性
- 操作元素常用属性 `对象.属性 = 值`
- 操作元素样式属性
    - 通过style属性操作CSS `对象.style.样式属性 = 值` 若属性有-连接符需要转换成小驼峰命名法
    - 操作类名操作CSS `元素.className = 'css类名'` className是使用新值换旧值，也就是覆盖以前的类名，若需要添加一个类，需要保留之前的类名
    - 通过classList操作类控制CSS
        - `元素.classList.add('css类名')` 追加一个类
        - `元素.classList.remove('css类名')` 删除一个类
        - `元素.classList.toggle('css类名')` 切换一个类
- 操作表单元素属性
    - 获取：`对象.属性名`
    - 设置：`对象.属性名 = 新值` 例如disabled、checked、selected等一律用布尔值表示，true表示添加了该属性，false代表移除该属性
- 自定义属性
    ```html
    // 标签一律以data-自定义属性格式，通过dataset对象方式获取
    <div class="box" data-id="10">盒子</div>
    <script>
        const box = document.querySelector('.box')
        console.log(box.dataset.id);
    </script>
    ```

### 定时器—间歇函数
1. 开启定时器 `setInterval(函数, 间隔时间)` 函数名不用加括号，间隔时间单位是毫秒，定时器返回的是一个id数字
2. 关闭定时器
    ```js
    let timer = setInterval(function(){
        console.log('hi');
    }, 1000)
    clearInterval(timer)
    ```

### 事件监听
**概念**：让程序检测是否有事件产生，一旦有事件触发，就立即调用一个函数做出响应，也称为 *绑定事件* 或 *注册事件*<br>
**三要素**：
1. 事件源
2. 事件类型
3. 事件调用的函数

**语法**：
1. 旧版本（L0） `元素对象.on事件 = function(){}`
2. 新版本（L2） `元素对象.addEventListener('事件类型', 要执行的函数)`

*注意：on方式会覆盖，而且只有冒泡阶段没有捕获，而addEventListener方式可绑定多次，拥有事件更多特性，推荐用新版本的

### 事件类型
1. 鼠标事件
    - click 鼠标点击
    - mouseenter 鼠标经过
    - mouseleave 鼠标离开
2. 焦点事件
    - focus 获得焦点
    - blur 失去焦点
3. 键盘事件
    - keydown 键盘按下触发
    - keyup 键盘抬起触发
4. 文本事件
    - input 用户输入事件

### 事件对象
**概念**：也是个对象，这个对象里有事件触发的相关信息，例如用户按下了键盘的哪个键<br>
**获取事件对象**： `元素对象.addEventListener('事件类型', function(e){})` 事件绑定的回调函数的第一个参数就是事件对象，一般命名为event、e<br>
**常见事件对象属性**： 
1. type 获取当前的事件类型
2. clientX/clientY 获取光标相对于浏览器可见窗口左上角的位置
3. offsetX/offsetY 获取光标相对于当前DOM元素左上角的位置
4. key 用户按下的键盘键的值

### 环境对象
**概念**：指的是函数内部特殊的变量this，它代表着当前函数运行时所处的环境。一般谁调用，this就是谁；直接调用函数，相当于是window.函数，所以this指代window

### 回调函数
**概念**：当函数A做为参数传递给函数B时，称函数A为回调函数

### 事件流
**概念**：事件完整执行过程中的流动路径。有两个阶段，分别是 *捕获阶段* 和 *冒泡阶段*，实际工作都是使用事件冒泡为主

<img src="https://i-blog.csdnimg.cn/direct/3a4c432cc0594fcba4dd921563e69e08.png#pic_center" width="400">

#### 事件捕获
**概念**：从DOM的根元素开始去执行对应的事件<br>
**语法**：`DOM.addEventListener('事件类型', 要执行的函数, 是否使用捕获机制)` 第三个参数传入true表示捕获阶段触发（很少使用），默认是false为冒泡阶段触发

#### 事件冒泡
**概念**：当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。也就是当一个元素触发事件后，会依次向上调用所有父级元素的同名事件（同种类型的事件）。默认存在

#### 阻止冒泡
1. 阻止事件冒泡 `事件对象.stopPropagation()` 此方法可以阻断时间流动传播，不光在冒泡阶段有效，捕获阶段也有效
2. 阻止默认行为（链接跳转，表单域跳转）发生 `e.preventDefault()`
    ```js
    const form = document.querySelector('form')
    form.addEventListener('click', function(e){
        e.preventDefault()
    })
    ```

#### 解绑事件
**语法**：`元素对象.removeEventListener('事件类型', 要执行的函数)` 注意匿名函数无法被解绑

### 事件委托
**优点**：减少注册次数，提高程序性能<br>
**原理**：利用事件冒泡特点，给父元素注册事件，当触发子元素时，会冒泡到父元素上，从而触发父元素的事件<br>
**语法**：`事件对象.target.tagName` 可获得真正触发事件的元素
```js
// 例如现在ul内存在li子元素
const ul = document.querySelector('ul')
ul.addEventListener('click', function(e){
    if(e.target.tagName === 'LI'){
        this.style.color = 'pink'
    }
})
```
### 页面加载事件
**概念**：加载外部资源（如图片、外联CSS和js等）加载完毕时触发的事件<br>
1. 监听页面所有资源加载完毕 `window.addEventListener('load',function(){})` 也可以针对某个资源绑定load事件
2. 初始HTML文档完全加载和解析完成后，无需等待样式表、图像等完全加载，即监听页面DOM加载完毕 `document.addEventListener('DOMContentLoaded',function(){})`

### 页面滚动事件
**概念**：滚动条在滚动的时候持续触发的事件<br>
**语法**：
1. 监听整个页面滚动 `window.addEventListener('scroll',function(){})` window或document添加scroll事件都行，也能监听某个元素内部滚动事件<br>
2. 获取滚动位置，有scrollLeft和scrollTop两个属性，获取被卷去的大小，这两个值是可读写的
    ```js
    // 例子1
    div.addEventListener('scroll', function(){
        // 尽量在scroll事件里获取被卷去的距离
        console.log(this.scrollTop)
    })

    // 例子2
    window.addEventListener('scroll', function(){
        // document.documentElement 是html元素获取方式
        const n = document.documentElement.scrollTop
        // n得到的是数字型，不带单位
        console.log(n)
    })
    ```
    <img src="https://i-blog.csdnimg.cn/direct/c7ccbdbb26f644c8bff8f9f24a2d946c.png#pic_center" width="400">
3. 滚动到指定坐标 `元素.scrollTo(x, y)`
    ```js
    // 让页面滚动到y轴1000像素的位置
    window.scrollTo(0, 1000)
    ```

### 页面尺寸事件
**语法**：
1. 窗口尺寸改变时触发事件 `window.addEventListener('resize', function(){})`
2. 检测屏幕宽度
    ```js
    window.addEventListener('resize', function(){
        let w = document.documentElement.clientWidth
        console.log(w)
    })
    ```
3. 获取元素宽高（不包含边框、margin、滚动条等）：`clientWidth`和`clientHeight` `元素.clientWidth`<br>
    <img src="https://i-blog.csdnimg.cn/direct/9b6175a7c7d949ec9c8d0129988bf1f6.png#pic_center" width="400">

### 元素尺寸与位置
1. 获取宽高（包含自身设置的宽高、padding、border）：`offsetWidth`和`offsetHeight` 获取的是数值，注意若盒子是隐藏的，结果是0 `元素.offsetWidth`
2. 获取位置：获取元素距离自己最近一级带有定位父级元素的左、上距离 `offsetLeft`和`offsetTop`是只读属性 `元素.offsetLeft`

### 日期对象
**方法**：
| 方法     | 作用     |说明     |
| -------- | -------- |-------- |
|getFullYear()| 获得年份 |获取四位年份 |
|getMonth()| 获得月份 |取值为0-11 |
|getDate()| 获取月份中的每一天 |不同月份取值也不相同 |
|getDay()| 获取星期 |取值为0-6 |
|getHours()| 获取小时 |取值为0-23 |
|getMinutes()| 获取分钟 |取值为0-59 |
|getSeconds()| 获取秒 |取值为0-59 |

**用法**：
1. 获取当前时间 `const data = new Data()` 用new关键词实例化一个日期对象
2. 获得指定时间 `const data = new Data('2008-8-8')`

#### 时间戳
**概念**：指的是1970年01月01日00时00分00秒起至现在的毫秒数<br>
**获取方法**：
1. 使用getTime()方法
    ```js
    const date = new Date()
    console.log(date.getTime())
    ```
2. 简写 `console.log(+new Date())`
3. 使用Date.now() `console.log(Date.now())` 但是只能得到当前的时间戳，而前面两种可以返回指定时间的时间戳

### DOM节点
**概念**：DOM树里每一个内容都称为节点<br>
**节点类型**：
- 元素节点（所有的标签，比如body、div，其中html是根节点）
- 属性节点（所有的属性，比如class属性）
- 文本节点（所有的文本，比如标签里的文字）
- 其他

**节点关系**：
- 父节点
- 子节点
- 兄弟节点

**查找节点**：
- 父节点查找 `子元素.parentNode` 返回最近一级的父节点，找不到返回null
- 子节点查找 
    - `父元素.childNodes` 获得所有子节点，包括文本节点（空格、换行）、注释节点等
    - `父元素.children` 仅获得所有元素节点，返回的还是一个伪数组
- 兄弟关系查找
    - 下一个兄弟节点 `nextElementSibling`属性
    - 上一个兄弟节点 `previousElementSibling`属性

**新增节点**：
- 创建节点 `document.createElement('标签名')`
- 追加节点
    - 插入到父元素的最后一个子元素 `父元素.appendChild(要插入的元素)`
    - 插入到父元素中某个子元素的前面 `父元素.insertBefore(要插入的元素, 在哪个元素前面)`
        ```js
        const ul = document.querySelector('ul')
        const li = document.createElement('li')
        li.innerHTML = 'li'
        ul.insertBefore(li, ul.children[0])
        ```
- 克隆节点 `元素.cloneNode(布尔值)` true则代表克隆会包含后代节点，false代表克隆不包含后代节点，默认为false

**删除节点**：`父元素.removeChild(要删除的元素)` 若不存在父子关系则删除不成功

### 移动端事件
| 触屏touch事件     | 说明     |
| -------- | -------- |
| touchstart| 手指触摸到一个DOM元素时触发 |
| touchmove| 手指在一个DOM元素上滑动时触发 |
| touchend| 手指从一个DOM元素上移开时触发 |

Swiper插件常用于移动端网站的内容触摸滑动

### BOM
**概念**：是浏览器对象模型。window对象是一个全局对象，像document、alert()、console.log()等这些都是window的属性。window对象下的属性和方法调用的时候可以省略window

<img src="https://i-blog.csdnimg.cn/direct/718d84b5e9c042f7bb1d1a5ec6a123e8.png#pic_center" width="600">

### 定时器—延时函数
1. 开启延时函数 `setTimeout(回调函数, 等待的毫秒数)` 仅仅只执行一次。就算等待的毫秒数为0，也会先执行之后的代码再执行函数里的代码
2. 清除延时函数
    ```js
    let timer = setTimeout(回调函数, 等待的毫秒数)
    clearTimeout(timer)
    ```
    *注意：每一次调用延时器都会产生一个新的延时器

### JS执行机制
**概念**：js语言的一大特点是单线程，同一个时间只能做一件事，为解决这个问题，利用多核CPU的计算能力，HTML5提出了Web Worker标准，允许JavaScript脚本创建多个线程，于是，JS中出现了同步和异步，这两种的本质区别是这条流水线上各个流程的执行顺序不同<br>
**同步**：前一个任务结束后在执行后一个任务，程序的执行顺序与任务排列顺序是一致的、同步的。同步任务都在主线程上执行，形成一个 *执行栈*<br>
**异步**：做这件事的同时，还可以去处理其他的事情。通过回调函数实现的。异步任务相关添加到 *任务列队*（也称为 *消息列队* ）<br>
**异步任务类型**：
1. 普通事件，如click、resize等
2. 资源加载，如load、error等
3. 定时器，如setInterval、setTimeout等

**js执行步骤**：
1. 先执行执行栈中的同步任务
2. 异步任务放入任务队列中
3. 一旦执行栈中所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行

<img src="https://i-blog.csdnimg.cn/direct/05177d3cead045efb175096df5280169.png#pic_center" width="900">

*注意：由于浏览器能处理多线程，所以图中web api部分的宿主是浏览器或node

**任务队列**：
1. 宏任务（Macro Task）：主线任务，如UI渲染、setTimeout、setInterval、事件回调 等
2. 微任务（Micro Task）：是比宏任务更“紧急”的任务，通常会在当前宏任务结束后立即执行，比下一次宏任务还早，如Promise.then/catch/finally、MutationObserver等

**事件循环 event loop**：主线程不断的重复获取任务、执行任务的这种机制称为事件循环

### location对象
**概念**：location的数据类型是对象，它拆分并保存了URL地址的各个组成部分<br>
**常用属性和方法**：
- herf属性
    ```js
    // 得到当前文件URL地址
    console.log(location.href)
    // 通过js方法跳转到目标地址
    location.href = 'http://...'
    ```
- search属性获取地址中携带的参数，符号？后面部分 `location.search`
- hash属性获取地址中的哈希值，符号#后面部分
- reload方法用来刷新当前页面，传入参数true时表示强制刷新 `location.reload()`

### navigator对象
**概念**：navigator的数据类型是对象，该对象下记录了浏览器自身的相关信息<br>
**常用属性**：userAgent属性检测浏览器的版本及平台 `navigator.userAgent`

### history对象
**概念**：history的数据类型是对象，主要管理历史记录，该对象与浏览器地址栏的操作相对应，如前进、后退、历史记录等。实际开发中用的较少<br>
**常用方法**：
| history对象方法     | 作用    |
| -------- | -------- |
| back()| 后退功能 |
| forward()| 前进功能 |
| go(参数)| 前进后退功能，参数若为1则前进1个页面，若为-1则后退1个页面 |

### 本地存储
1. 数据存储在用户浏览器中
2. 设置、读取方便，页面刷新不丢失数据
3. 容量大，sessionStorage和localStorage约5M左右

**分类**：
1. **localStorage**：用localStorage把数据存储在本地（用户电脑），除非手动删除，否则关闭页面也会存在。可以多窗口共享（同一浏览器可以共享），以键值对的形式存储使用。本地存储只能存储字符串数据类型。通过F12中的application查看本地数据
    - 存储数据 `localStorage.setItem('key', 'value')` 若原来有这个key，则是改，如果没有这个key则是增
    - 获取数据 `localStorage.getItem('key')` 若对应value获取不到，则返回值是null
    - 删除数据 `localStorage.removeItem('key')`
    - 清空数据 `localStorage.clear()`

2. **sessionStorage**：生命周期为关闭浏览器窗口，在同一个窗口（页面）下数据可以共享，以键值对的形式存储使用，用法和localStorage基本相同

**存储复杂数据类型**：
- 存储数据：将复杂数据类型转换成JSON字符串，在存储到本地
    ```js
    const goods = {
        name:'wu',
        age:18
    }
    localStorage.setItem('goods', JSON.stringify(goods))
    ```
- 获取数据：因为本地存储里取出来的是字符串不是对象，无法直接使用，所以要把取出来的字符串转换成对象
    ```js
    const obj = JSON.parse(localStorage.getItem('goods'))
    console.log(obj)
    ```

### 正则表达式
**概念**：用于匹配字符串中字符组合的模式。在JS中，正则表达式也是对象。通常用来查找、替换那些符合正则表达式的文本，许多语言都支持正则表达式<br>
**使用场景**：
- 表单验证（匹配）
- 过滤敏感词（替换）
- 字符串中提取想要的部分（提取）

**语法**：
- 定义正则表达式 `const 变量名 = /表达式/` 其中/ /是正则表达式字面量
- 判断是否有符合规则的字符串 `变量名.test(被检测的字符串)` 符合返回true，否则为false
    ```js
    const str = '啊哈哈哈哈哈哈前端哈哈哈'
    const reg = /前端/
    console.log(reg.test(str))// true
    ```
- 检索符合规则的字符串 `变量名.exec(被检测的字符串)` 匹配成功返回一个数组（包含找到的第一个符合规则的索引号等），否则返回null

#### 元字符
**概念**：一些具有特殊含义的字符，极大提高灵活性和强大的匹配功能，例如普通字符的26个英文字符 abcd...，但是换成元字符写法 [a-z]<br>
**分类**：
- 边界符：表示位置，若两个一起使用，表示必须是精确匹配

    | 边界符     | 说明     |
    | -------- | -------- |
    | ^| 表示匹配行首的文本 |
    | $| 表示匹配行尾的文本 |

- 量词：表示重复次数

    | 量词     | 说明     |
    | -------- | -------- |
    | *| 重复零次或更多次 |
    | +| 重复一次或更多次 |
    | ？| 重复零次或一次 |
    | {n}| 重复n次 |
    | {n,}| 重复n次或更多次 |
    | {n,m}| 重复n到m次 |

- 字符类：比如 \d 表示0~9
    - [] 只要中括号内的任意字符出现都返回true
    - [-] 使用连字符-表示一个范围
        - [a-z] 表示a到z26个英文字母都可以
        - [a-zA-Z] 表示a到z26个英文字母大小写都可以
        - [0-9] 表示0到9数字都可以
    - [^] 取反
        - [^a-z] 表示除了小写字母以外的字符
    - . 点匹配除换行符之外的任何单个字符
    - 预定义：指的是某些常见模式的简写方式

        | 预定义类     | 说明     |
        | -------- | -------- |
        | \d| 匹配0~9之间任一数字 |
        | \D| 匹配除了0~9以外的字符 |
        | \w| 匹配任意字母、数字和下划线 |
        | \W| 匹配除了字母、数字和下划线以外的字符 |
        | \s| 匹配空格（包括换行符、制表符、空格符等） |
        | \S| 匹配非空格的字符 |
```js
console.log(/^[1-9][0-9]{4,}/.test('10000'))// 表示从10000开始，结果为true
```

#### 修饰符
**概念**：修饰符约束正则执行的某些细节行为，如是否区分大小写、是否支持多行匹配等<br>
**语法**：
- `/正则表达式/i` 正则匹配时字母不区分大小写
- `/正则表达式/g` 匹配所有满足正则表达式的结果
- `字符串.replace(/正则表达式/, '替换的文本')` replace替换
    ```js
    const str = 'java编程语言，学JAVA'
    // 若这里不加g，则只会替换找到的第一个符合的
    const re = str.replace(/java/ig, '前端')
    console.log(re)// 前端编程语言，学前端
    ```

## JS进阶
### 内存的生命周期
1. 内存分配：当我们声明变量、函数、对象的时候，系统会自动为他们分配内存
2. 内存使用：即读写内存，也就是使用变量、函数等
3. 内存回收：使用完毕，由垃圾回收器自动回收不再使用的内存

*注意：全局变量一般不会回收（关闭页面回收）。一般情况下局部变量的值不用了会被自动回收掉

**内存泄露**：程序中分配的内存由于某种原因，程序未释放或无法释放

### 垃圾回收机制GC
**概念**：js中内存的分配和回收都是自动完成的，内存在不使用的时候会被垃圾回收器自动回收<br>
**堆栈空间分配区别**：
- 栈（操作系统）：由操作系统自动分配释放函数的参数值、局部变量等
- 堆（操作系统）：一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收

**常见算法**：
- 引用计数法（不再使用）：看一个对象是否有指向它的引用，没有引用了就回收对象。但存在嵌套引用（循环引用）的问题，即若两个对象相互引用，尽管它们已不再使用，垃圾回收器不会进行回收，导致内存泄露
    1. 跟踪记录被引用的次数
    2. 如果被引用了一次，那就记录次数1，多次引用会累加 ++
    3. 如果减少一个引用就减1 --
    4. 如果引用次数是0，则释放内存
- 标记清除法（浏览器通用的大多是基于该算法的改进算法）：将不再使用的对象定义为无法到达的对象，从根部（在js中就是全局对象）出发定时扫描内存中的对象，凡是能从根部到达的对象，都是还需要使用的，那些无法从根部触发触及到的对象被标记为不再使用，稍后进行回收<br>
<img src="https://i-blog.csdnimg.cn/direct/6f85dfb3fbb54c32abfb96d74ab9e85e.png#pic_center" width="500">

    ```js
    function fn(){
        let o1 = {}
        let o2 = {}
        o1.a = o2
        o2.a = o1
        return '引用计数无法回收，标记清除可以回收'
    }
    fn()
    ```

### 闭包Closure
**概念**：一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域。简单来说就是 闭包=内层函数+外层函数的变量<br>
**作用**：封闭数据，实现数据私有，外部也可以访问函数内部的变量<br>
**可能引起的问题**：内存泄漏<br>
**基本格式**：
```js
function outer(){
    let i = 1
    function fn(){
        console.log(i)
    }
    return fn
}
const fun = outer()
fun()
```

### 变量提升
**概念**：允许在变量声明之前被访问（仅存在于var声明变量）。变量在var声明前被访问，变量值为undefined，即只提升变量声明，不提升变量赋值。变量提升出现在相同作用域中（不建议使用）

### 函数提升
**概念**：指函数在声明之前被调用。函数提升出现在相同作用域中
```js
foo()
function foo(){
    console.log('函数提升')
}

// 函数表达式不存在提升现象
bar()// 错误
var bar = function(){
    console.log('函数提升')
}
```

### 函数参数
1. 动态参数
    - arguments是函数内部内置的伪数组变量，包含了调用函数时传入的所有实参。作用是动态获取函数的实参。只存在于函数中
        ```js
        function sum(){
            console.log(arguments) 
            let sum = 0
            for(let i = 0; i < arguments.length; i++){
                sum += arguments[i]
            }
            console.log(sum)
        }
        sum(1, 2, 3)
        ```
2. 剩余参数（提倡）：允许将一个不定数量的参数表示成一个数组。...置于最末函数形参之前，用于获取多余的实参，借助...获取的剩余实参，是个真数组
    ```js
    function sum(one, ...other){
        console.log(one)// 得到1
        console.log(other) // 得到[2,3]
    }
    sum(1, 2, 3)
    ```

### 展开运算符...
**概念**：将一个数组进行展开<br>
**典型运用场景**：
- 求数组最大值或最小值
    ```js
    const arr = [1, 2, 3]
    console.log(Math.max(...arr)) // 3
    console.log(Math.min(...arr)) // 1
    ```
- 合并数组
    ```js
    const arr1 = [1, 2, 3]
    const arr2 = [4, 5, 6]
    const arr3 = [...arr1, ...arr2]
    console.log(arr3)// [1,2,3,4,5,6]
    ```

### 箭头函数
**作用**：更简短的函数写法并且不绑定this。适用于那些本来需要匿名函数的地方。属于表达式函数，因此不存在函数提升<br>
**语法**：
- 语法1
    ```js
    const fn = () => {
        console.log('箭头函数')
    }
    fn()
    ```
- 语法2：只有一个参数可省略小括号
    ```js
    const fn = x => {
        return x + x
    }
    console.log(fn(1))// 2
    ```
- 语法3：若函数体只有一行代码，可以写到一行上，无需写return直接返回值
    ```js
    const fn = (x, y) => x + y
    console.log(fn(1, 2))// 3
    ```
- 语法4：加括号的函数体返回对象字面量表达式
    ```js
    const fn = uname => ({uname: uname})
    console.log(fn('wu'))// { uname: 'wu' }
    ```

**箭头函数参数**：没有arguments动态参数，但是有剩余参数...args
```js
const sum = (...args) => {
    let sum = 0
    for(let i = 0; i < args.length; i++){
        sum += args[i]
    }
    return sum
}
console.log(sum(1,2,3))// 6
```
**箭头函数this**：箭头函数不会创建自己的this，它只会从自己的作用域链的上一层沿用this
```js
console.log(this)// 指向window
const say = () => {
    console.log(this)// 指向window
}
btn.addEventListener('click', () => {
    console.log(this)// 指向window
})

const user = {
    name: 'wu',
    walk: () => {
        console.log(this)// 指向window
    }
}
user.walk()
```
*注意：事件回调函数使用箭头函数时，this为全局的window，因此DOM事件回调函数为了简便，还是不太推荐使用箭头函数

### 数组解构
**概念**：将数组的单元值快速批量赋值给一系列变量的简洁语法<br>
**语法**：
1. 赋值运算符 = 左侧的 [ ] 用于批量声明变量，右侧数组的单元值将被赋值给左侧的变量
    ```js
    const arr = [1,2,3]
    const [a,b,c] = arr
    console.log(a)// 1
    console.log(b)// 2
    console.log(c)// 3
    ```
2. 变量的顺序对应数组单元值的位置依次进行赋值操作。若单元值少，变量多的情况，则多出的变量为undefined；若单元值多，变量少的情况，可以用剩余参数解决
    ```js
    // 1 2 3是单元值
    const [a,b,c] = [1,2,3]
    console.log(a)// 1
    console.log(b)// 2
    console.log(c)// 3

    // 按需导入，忽略某些返回值
    const [a, ,c,d] = [1,2,3,4]
    console.log(a)// 1
    console.log(c)// 3
    console.log(d)// 4

    // 支持多维数组
    const [a,b] = ['苹果',['小米','华为']]
    console.log(a)// 苹果
    console.log(b)// ['小米','华为']

    const [a,[b,c]] = ['苹果',['小米','华为']]
    console.log(a)// 苹果
    console.log(b)// 小米
    console.log(c)// 华为
    ```
*注意：为了防止有undefined传递单元值的情况，可以设置默认值

**典型应用**：交换两个变量
```js
let a = 1
let b = 3; //这里必须有分号
[b,a] = [a,b]
console.log(a)// 3
console.log(b)// 1
```

### 对象解构
**概念**：将对象属性和方法快速批量赋值给一系列变量的简洁语法<br>
**语法**：
1. 赋值运算符 = 左侧的 { } 用于批量声明变量，右侧对象的属性值将被赋值给左侧的变量。对象属性的值将被赋值给与属性名相同的变量。解构的变量名不要和外面的变量名冲突否则会报错。对象中找不到与变量名一致的属性时变量值为undefined
    ```js
    const user = {
        name:'wu',
        age:18
    };
    const {name, age} = user
    console.log(name)// wu
    console.log(age)// 18
    ```
2. 给新的变量名赋值
    ```js
    const user = {
        name:'wu',
        age:18
    };
    const {name: uname, age} = user
    console.log(uname)// wu
    console.log(age)// 18
    ```
3. 数组对象解构
    ```js
    const user = [
        {
            name:'wu',
            age:18
        }
    ]
    const [{name, age}] = user
    console.log(name, age)
    ```
4. 多级对象解构
    ```js
    const user = {
        name: 'wu',
        family:{
            mother: 'z',
            father:'w'
        }
    }
    const {name, family:{mother, father}} = user
    console.log(name, mother, father)
    ```

### 实例成员
**概念**：通过构造函数创建的对象称为实例对象，实例对象中的属性和方法称为实例成员（实例属性和实例方法）<br>
**语法**：
```js
function Person(){
    // 构造函数内部的this就是实例对象
    // 实例对象中动态添加属性
    this.name = '小明'
    // 实例对象动态添加方法
    this.sayHi = function(){
        console.log('你好')
    }
}
// 实例化，p1是实例对象
const p1 = new Person()
console.log(p1)
console.log(p1.name) // 访问示例属性
p1.sayHi() // 调用示例方法
```
*注意：为构造函数传入参数，创建结构相同但值不同的对象；构造函数创建的实例对象彼此独立互不影响

### 静态成员
**概念**：构造函数的属性和方法称为静态成员（静态属性和静态方法），如Data.now()、Math.PI、Math.random()<br>
**语法**：
```js
function Person(name, age){
    // 省略实例成员
}
// 静态属性
Person.eyes = 2
// 静态方法
Person.walk = function(){
    console.log('走路')
    // this指向Person
    console.log(this.eyes)
}
```
*注意：静态成员只能构造函数来访问；静态方法中的this指向构造函数

### 内置构造函数
**概念**：字符串、数值、布尔等基本类型也有专门的构造函数，这些我们称为包装类型。JS中几乎所有的数据都可以基于构造函数创建
```js
const str = 'pink'
// js底层完成，把简单数据类型包装成引用数据类型，相当于const str = new String('pink')
console.log(str.length)
```
**分类**：
- 引用类型
    - Object：创建普通对象
        - Object.keys静态方法获取对象中所有属性（键），返回一个数组
            ```js
            const o = {name:'wu', age:18}
            // 获取对象的所有键，并返回的是一个数组
            const arr = Object.keys(o)
            console.log(arr) // ['name', 'age']
            ```
        - Object.values静态方法获取对象中所有属性值，返回一个数组
        - Object.assign静态方法用于对象拷贝
            ```js
            // 场景1：把o拷贝给obj
            const o = {name:'wu', age:18}
            const obj = {}
            Object.assign(obj, o)
            console.log(obj) // {name:'wu', age:18}

            // 场景2(常用)：给对象添加属性
            const o = {name:'wu', age:18}
            Object.assign(o, {gender:'女'})
            console.log(obj) // {name:'wu', age:18, gender:'女'}
            ```
    - Array：创建数组
        - forEach遍历数组，不返回数组，常用于查找遍历数组元素
        - filter过滤数组，返回新数组，返回筛选满足条件的数组元素
        - map迭代数组，返回新数组，返回处理后的数组元素
        - reduce累计器，返回累计处理的结果，常用于求和等 `arr.reduce(function(上一次值,当前值){}, 起始值)` 初始值可选
            ```js
            const arr = [1, 2, 3]
            // reduce执行过程：若无初始值，则上一次值以数组的第一个元素的值，每一次循环，把返回值给作为下一次循环的上一次值；若有初始值，则起始值作为上一次值
            const total = arr.reduce((prev, current) => prev + current, 10)
            console.log(total) // 16
            ```
        - join将数组元素拼接为字符串，返回字符串
        - find查找元素，返回符合条件的第一个数组元素值，若没有符合条件的则返回undefined
            ```js
            const arr = [
                {
                    name:'小米',
                    price:1999
                },
                {
                    name:'华为',
                    price:3999
                },
            ]
            const mi = arr.find(item => item.name === '小米')
            console.log(mi) // {name:'小米', price:1999}
            ```
        - every检测数组所有元素是否都符合指定条件，若都通过返回true，否则返回false
            ```js
            const arr = [10, 20]
            const flag = arr.every(item => item >= 10)
            console.log(flag) // true
            ```
        - some检测数组中的元素是否符合指定条件，若数组中有元素符合就返回true，否则返回false
        - concat合并两个数组，返回生成的新数组
        - sort对原数组单元值排序
        - splice删除或替换原数组单元
        - reverse反转数组
        - findIndex查找元素的索引值
    - RegExp，Data等
- 包装类型
    - String：创建字符串
        - length用来获取字符串长度
        - split用来将字符串拆分成数组 `split('分隔符')`
            ```js
            const str = 'pink,red'
            const arr = str.split(',')
            console.log(arr) // ['pink','red']
            ```
        - substring用于字符串截取 `substring(需要截取的第一个字符的索引[,结束的索引号])`
            ```js
            const str = '你好呀'
            // 若省略结束的索引号，默认取到最后；结束的索引号不包含想要截取的部分
            console.log(str.substring(1, 2)) // 好
            ```
        - startsWith检测是否以某字符开头 `startsWith(检测字符串[,检测位置索引号])`
            ```js
            const str = '你好呀'
            console.log(str.startsWith('你')) // true
            ```
        - includes判断一个字符串是否包含在另一个字符串中，根据情况返回true或false `includes(搜索的字符串[,检测位置索引号])`
            ```js
            const str = '你好呀'
            console.log(str.includes('好')) // true
            ```
        - toUpperCase用于将字母转换成大写
        - toLowerCase用于将字母转换成小写
        - indexOf检测是否包含某字符
        - endsWith检测是否以某字符结束
        - replace用于替换字符串，支持正则匹配
        - match用于查找字符串，支持正则匹配
    - Number：创建数值
        - toFixed设置保留小数位的长度
            ```js
            const price = 12.345
            // 保留两位小数，四舍五入
            console.log(price.toFixed(2)) // 12.35
            ```
    - Boolean等

**构造函数**：js面向对象可以通过构造函数实现封装，但存在浪费内存的问题<br>
<img src="https://i-blog.csdnimg.cn/direct/d6120b1717134ce1a1d09172817de950.png#pic_center" width="800">

### 编程思想
1. **面向过程编程（POP）**：面向过程就是按照分析好的步骤解决问题
- 优点：性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向对象编程
- 缺点：没有面向对象易维护、易复用、易扩展
2. **面向对象编程（OOP）**：面向对象就是以对象功能来划分问题，而不是步骤。每一个对象都是功能中心，具有明确分工
- 优点：易维护、易复用、易扩展，由于面向对象有 *封装性*、*继承性*、*多态性* 的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护<br>
<img src="https://i-blog.csdnimg.cn/direct/5e93488f622e4d55a725390de9bcfb9a.png#pic_center" width="450">
- 缺点：性能比面向过程低

### 原型
**目标**：利用原型对象实现方法共享，也就是解决构造函数存在浪费内存的问题<br>
**概念**：
- 构造函数通过原型分配的函数是所有对象所共享的
- js中规定，每一个构造函数都有一个prototype属性，指向另一个对象，所以我们也称为原型对象
- 这个对象可以挂载函数，对象实例化不会多次创建原型上函数，节约内存
- 可以把那些不变的方法，直接定义在prototype对象上，这样所有对象的实例就可以共享这些方法
- 构造函数和原型对象中的this都指向实例化的对象

**语法**：
```js
// 1.公共的属性写到构造函数内
function Star(uname, age){
    this.uname = uname
    this.age = age
}
// 2.公共的方法写到原型对象身上
Star.prototype.sing = function(){
    console.log('唱歌')
}
const ldh = new Star('刘德华', 55)
const zxy = new Star('张学友', 58)
ldh.sing() // 唱歌
zxy.sing() // 唱歌
console.log(ldh.sing === zxy.sing) // true
```
<img src="https://i-blog.csdnimg.cn/direct/577ca985b8614531b8b96a94f7807dc8.png#pic_center" width="550">

#### constructor属性
**概念**：每个原型对象里都有个constructor属性，该属性指向该原型对象的构造函数

<img src="https://i-blog.csdnimg.cn/direct/d3f97ec2d6e941d6ac0506e1f9bca009.png#pic_center" width="600">

**使用场景**：若有多个对象的方法，可以给原型对象采取对象形式赋值，但这样会覆盖构造函数原型对象原来的内容，此时我们可在修改后的原型对象中，添加一个constructor指向原来的构造函数

<img src="https://i-blog.csdnimg.cn/direct/343105153d414528bd0367621c475305.png#pic_center" width="1000">

**存在**：*prototype原型* 和 *对象原型__proto__* 里都有

#### __proto__属性
**概念**：对象都有一个属性__proto__指向构造函数的prototype原型对象，因为有了这个的存在，所以对象可以使用构造函数prototype原型对象的属性和方法

<img src="https://i-blog.csdnimg.cn/direct/a16d4ccd2846490b876c3a51efcbdf44.png#pic_center" width="600">

*注意：
- __proto__是JS非标准属性
- [[prototype]]和__proto__意义相同
- 用来表明当前实例对象指向哪个原型对象prototype
- __proto__对象原型里面也有一个constructor属性，指向创建该实例对象的构造函数

#### 原型继承
**概念**：继承是面向对象编程的另一个特征，通过继承进一步提升代码封装的程度，JS中大多是借助原型对象实现继承<br>
**语法**：
```js
function Person(){
    this.eyes = 2
}
function Woman(){}
// Woman通过原型来继承Person。若Woman.prototype = Person会导致修改Woman.prototype时会直接修改Person
Woman.prototype = new Person()
// 指回原来的构造函数
Woman.prototype.constructor = Woman
```

#### 原型链
**概念**：基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对象的链状结构关系称为原型链

<img src="https://i-blog.csdnimg.cn/direct/5daa5f628b4e431d9ddf40f5bf8354a0.png#pic_center" width="800">

**查找规则**：
1. 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性
2. 如果没有就查找它的原型（也就是__proto__指向的prototype原型对象）
3. 如果还没有就查找原型对象的原型（Object的原型对象）
4. 依次类推一直找到Object为止（null）

```js
function Person(){
    this.eyes = 2
}
const ldh = new Person()
console.log(ldh.__proto__ === Person.prototype) //true
console.log(Person.prototype.__proto__ === Object.prototype) //true
// 可以使用instanceof运算符用于检测构造函数的prototype属性是否出现在某个实例对象的原型链上
console.log(ldh instanceof Person) // true
console.log(ldh instanceof Object) // true
```

*注意： __proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线

### 浅拷贝
**概念**：简单数据类型拷贝值，引用数据类型拷贝的是地址<br>
**常见方法**：
1. 拷贝对象：Object.assign() 或者 用展开运算符{...obj}
    ```js
    const obj = {
        age: 18
    }
    // 若是直接赋值o = obj，修改age会修改obj，因为直接拷贝对象栈里面的地址
    // 若obj中还有方法，以下两种方法修改方法会影响obj
    // 方法1：Object.assign()
    const o = {}
    Object.assign(o, obj)
    console.log(o) // {age:18}

    // 方法2：展开运算符{...obj}
    const o = {...obj}
    console.log(o) // {age:18}
    o.age = 20
    console.log(o) // {age:20}
    console.log(obj) // {age:18}
    ```
2. 拷贝数组：Array.prototype.concat() 或者 [...arr]

### 深拷贝
**概念**：拷贝的是对象，不是地址<br>
**常见方法**：
1. 通过递归实现深拷贝：函数内部自己调用自己，这个函数就是递归函数。递归函数的作用和循环效果类似。由于递归易发生“栈溢出”（stack overflow）错误，所以必须加退出条件return
    ```js
    const obj = {
        uname:'pink',
        age:18,
        hobby:['乒乓球', '足球'],
        family:{
            baby:'小pink'
        }
    }
    const o = {}
    function deepCopy(newObj, oldObj){
        for(let k in oldObj){
            // 这里一定要注意先判断是否是数组再判断是否是对象，因为数组也属于对象，[1,2] instanceof Object会返回true
            if(oldObj[k] instanceof Array){
                newObj[k] = []
                deepCopy(newObj[k], oldObj[k])
            }else if(oldObj[k] instanceof Object){
                newObj[k] = {}
                deepCopy(newObj[k], oldObj[k])
            }else{
                // k是属性名，oldObj[k]是属性值
                // newObj[k] === o.uname 给新对象添加属性
                newObj[k] = oldObj[k]
            }
        }
    }
    deepCopy(o, obj)
    ```
2. js库lodash里的cloneDeep内部实现了深拷贝：_.cloneDeep(要被克隆的对象)
    ```js
    const obj = {
        uname:'pink',
        age:18,
        hobby:['乒乓球', '足球'],
        family:{
            baby:'小pink'
        }
    }
    const o = _.cloneDeep(obj)
    ```
3. 通过JSON.stringify()实现
    ```js
    const obj = {
        uname:'pink',
        age:18,
        hobby:['乒乓球', '足球'],
        family:{
            baby:'小pink'
        }
    }
    // 先把对象转换成JSON字符串再用parse解析成js对象或值
    const o = JSON.parse(JSON.stringify(obj))
    ```

### 异常处理
**概念**：异常处理是指预估代码执行过程中可能发生的错误，然后最大程度的避免错误的发生导致整个程序无法继续运行<br>
**常见方法**：
1. throw抛异常
    ```js
    function counter(x, y){
        if(!x || !y){
            // throw抛出异常信息，程序也会终止执行
            // Error对象配合throw使用，能够设置更详细的错误信息
            throw new Error('参数不能为空')
        }
        return x + y
    }
    counter()
    ```
2. try/catch捕获异常
    ```js
    function foo(){
        try{
            // 可能出错的代码写到try内
            const p = document.querySelector('.p')
            p.style.color = 'red'
        }catch(err){
            // try代码中出现错误，会执行catch代码段，并截获到错误信息，但是不终止程序继续执行
            console.log(err.message)
            // 中断程序需要加return,或者配合throw使用，两种选择一个即可
            throw new Error('参数不能为空')
            // return
        }
        finally{
            // finally不管是否有错误，都会执行
            alert('执行')
        }
        console.log('若出现错误，该语句不会执行') 
    }
    foo()
    ```
3. debugger

### 处理this
**this指向**：
- 普通函数：普通函数的调用方式决定了this的值，即谁调用this的值就指向谁。普通函数没有明确调用者时this值为window，严格模式下（'use strict'）没有调用者时this的值为undefined
    ```js
    // 情形1
    console.log(this) // window

    // 情形2
    function fn(){
        console.log(this) // window
    }
    fn()

    // 情形3
    setTimeout(function(){
        console.log(this) // window
    }, 1000)

    // 情形4
    document.querySelector('button').addEventListener('click', function(){
        console.log(this) // button
    })

    // 情形5
    const obj = {
        sayHi:function(){
            console.log(this) // obj
        }
    }
    obj.sayHi()
    ```
- 箭头函数：箭头函数中不存在this，沿用上一级的，向外层作用域中，一层一层查找this，直到有this的定义
    ```js
    // 情形1
    const sayHi = function(){
        console.log(this) // window
    }

    // 情形2
    const obj = {
        sayHi:() => {
            console.log(this) // window
        }
    }

    // 情形3：dom事件函数
    document.querySelector('button').addEventListener('click', function(){
        console.log(this) // window
    })

    // 情形4：原型函数
    function Person(){}
    Person.prototype.walk = () => {
        console.log(this) // window
    }
    const p1 = new Person()
    p1.walk()
    ```
**改变this指向**：
1. function.call(thisArg, arg1, arg2, ...)：其中thisArg指的是在function函数运行时指定的this值。返回值就是函数的返回值，因为它就是调用函数（了解）
    ```js
    const obj = {
        uname:'pink'
    }
    function fn(x, y){
        console.log(this) 
        console.log(x + y)
    }
    fn.call(obj, 1, 2) // this指向obj 且 输出3
    ```
2. function.apply(thisArg,[argsArray])：其中thisArg指的是在function函数运行时指定的this值。argsArray是传递的值，必须包含在数组里面。返回值就是函数的返回值，因为它就是调用函数
    ```js
    const obj = {
        uname:'pink'
    }
    function fn(x, y){
        console.log(this) 
        console.log(x + y)
    }
    fn.apply(obj, [1, 2]) // this指向obj 且 输出3

    // 使用场景：求数组最大值( 另一种方法是 Math.max(...arr) )
    const arr = [100, 33, 3]
    const max = Math.max.apply(Math, arr)
    console.log(max) // 100
    ```
3. function.bind(thisArg, arg1, arg2, ...)：该方法不会调用函数。其中thisArg指的是在function函数运行时指定的this值。返回由指定的this值和初始化参数改造的原函数拷贝（新函数）
    ```js
    const obj = {
        uname:'pink'
    }
    function fn(){
        console.log(this) 
    }
    const fun = fn.bind(obj)
    // 调用利用bind创建的新函数fun，其构造与fn一样
    fun() // {uname:'pink'}

    // 使用场景：有一个按钮，点击后就禁用，2秒后开启
    document.querySelector('button').addEventListener('click', function(){
        this.disabled = true // 这里的this指向button
        window.setTimeout(function(){
            // bind将this由原来的window 改为 button
            this.disabled = false
        }.bind(this), 2000)
    })
    ```
**改变this指向的三种方法总结**：
- 相同点：都改变this指向
- 区别点：call和apply会调用函数，而bind不会调用函数。call和apply传递参数不同，apply传递必须是数组形式

### 性能优化
#### 防抖（debounce）
**概念**：单位时间内，频繁触发事件，只执行最后一次

<img src="https://i-blog.csdnimg.cn/direct/b38b846092f84e3ca31ac30b6a59991c.png#pic_center" width="390">

**使用场景**：
1. 搜索框只需在用户最后一次输入完再发送请求
2. 手机号、邮箱验证输入检测

**实现方式**：
1. lodash提供的防抖处理：_.debounce(function, time) 注意这里time是毫秒
    ```js
    // 需求：页面一个盒子，里面有数字，实现鼠标在盒子内移动，鼠标停止500ms后，数字+1
    const box = document.querySelector('.box')
    let i = 1
    function mouseMove(){
        box.innerHTML = i++
        // 若存在开销较大操作，大量数据处理，大量dom操作，可能会卡
    }
    box.addEventListener('mousemove', _.debounce(mouseMove, 500))
    ```
2. 手写一个防抖函数处理：核心是利用setTimerout定时器来实现
    ```js
    function debounce(fn, t){
        // 1. 声明定时器变量
        let timer
        // return返回一个匿名函数
        return function(){
            // 2. 每次事件触发的时候先判断是否有定时器，如果有先清除以前的定时器
            if(timer) clearTimeout(timer)
            // 3. 如果没有定时器，则开启定时器，存入到定时器变量里面
            timer = setTimeout(function(){
                fn()
            }, t)
        }
    }
    box.addEventListener('mousemove', debounce(mouseMove, 500))
    ```

#### 节流（throttle）
**概念**：单位时间内，频繁触发事件，只执行一次

<img src="https://i-blog.csdnimg.cn/direct/8121dce3e79f470d9ed668818b7cea67.png#pic_center" width="390">

**使用场景**：高频事件如鼠标移动mousemove、页面尺寸缩放resize、滚动条滚动scroll 等<br>
**实现方式**：
1. lodash提供的节流函数处理：_.throttle(function, time) 注意这里time是毫秒
    ```js
    // 需求：页面一个盒子，里面有数字，实现鼠标在盒子内移动，不管移动多少次，每隔500ms数字才+1
    const box = document.querySelector('.box')
    let i = 1
    function mouseMove(){
        box.innerHTML = i++
        // 若存在开销较大操作，大量数据处理，大量dom操作，可能会卡
    }
    box.addEventListener('mousemove', _.throttle(mouseMove, 500))
    ```
2. 手写一个节流函数处理：核心是利用setTimerout定时器来实现
    ```js
    function throttle(fn, t){
        // 1. 声明定时器变量
        let timer = null
        // return返回一个匿名函数
        return function(){
            // 2. 每次事件触发的时候先判断是否有定时器，如果有定时器则不开启新定时器
            // 3. 如果没有定时器则开启定时器
            if(!timer){
                timer = setTimeout(function(){
                    fn()
                    // 清除定时器。不用clearTimeout(timer)是因为setTimeout中定时器还在运作无法删除
                    timer = null
                }, t)
            }
        }
    }
    box.addEventListener('mousemove', throttle(mouseMove, 500))
    ```