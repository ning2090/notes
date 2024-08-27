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
**用法**：与变量类似
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
**概念**：某些运算符被执行时，系统内部自动将数据类型进行转换
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
    console.log(j++ + 1);// 结果2。i先和2相加，运算完输出完毕后，i再自加变成2
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
    - `arr.splice(操作的下标, 删除的个数)` 指定删除，其中删除的个数可选，不写删除的个数默认删除到最后
7. 数组排序（与冒泡排序（两个两个比较，先排序完一个再看另一个）后结果相同，直接修改原数组，而不是返回一个新数组）
    ```js
    // 升序
    arr.sort((a, b) => a - b) 
    // 降序
    arr.sort((a, b) => b - a)
    ```
8. 遍历数组
    ```js
    for(let i = 0; i < 数组名.length; i++){
        数组名[i]
    }
    ```

## 对象
**概念**：无序的数据集合
1. 声明语法({}是对象字面量。对象由属性和方法组成)
    - 方法1：`let 对象名 = {属性名: 属性值, 方法名: 函数}`
    - 方法2：`let 对象名 = new Object()`
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
- 全局作用域：函数外部或者整个script有效
    - 全局变量
- 局部作用域：也称函数作用域，函数内部有效
    - 局部变量

### 变量的访问原则
- 只要是代码就至少有一个作用域
- 写在函数内部的局部作用域
- 如果函数中还有函数，那么在这个作用域中又可以诞生一个作用域
- 访问原则：在能够访问到的情况下，先局部再找全局

## 逻辑中断
- 逻辑运算符里的短路，只存在于&&和||中
    - && 左边为false就短路，即右边不执行。两边都为真，返回最后一个真值
    - || 左边为true就短路。两边都为真，返回第一个真值

## 堆栈空间
1. 栈（操作系统）：由操作系统自动分配释放存放函数的参数值、局部变量的值等。简单数据类型会存放到栈里
2. 堆（操作系统）：存储复杂类型（对象），一般又程序员分配释放，若不释放，则由垃圾回收机制回收

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
    - `document.querySelectorAll('css选择器')` 选择匹配的多个元素，返回的是NodeList对象集合，得到的是一个伪数组。参数包含一个或多个有效的CSS选择器字符串。不能直接修改，需要通过遍历的方式给里面的元素做修改
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
**概念**：让程序检测是否有事件产生，一旦有事件触发，就立即调用一个函数做出响应，也成为 *绑定事件* 或 *注册事件*<br>
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
**概念**：事件完整执行过程中的流动路径。有两个阶段，分别是捕获阶段和冒泡阶段，实际工作都是使用事件冒泡为主

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