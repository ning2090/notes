# 搭建
create-react-app是一个快速 *创建React开发环境的工具* ，底层由Webpack构建，封装了配置细节。<br>
`npx create-react-app 项目名`<br>
npx : Node.js工具命令，查找并执行后续的包命令

把app根组件先引入到index.js中，再渲染到public文件夹下的index.html的id为root的dom节点上

# JSX
**概念**：是JavaScript和XML(HTML)的缩写，表示在 *JS代码中编写HTML模板结构*，是React中编写UI模板的方式<br>
**优势**：1.HTML的声明式模板写法 2.JS的可编程能力<br>
**本质**：不是标准JS语法，是JS的语法扩展，浏览器需要通过解析工具解析后才能运行(*BABEL*)<br>
**语法规范**：
1. 标签中混入JS表达式用{}
2. 样式类名不用class而是className
3. 内联样式用style={{color:'red'}}的形式
4. 只有一个根标签
5. 标签必须闭合
6. 标签首字母若小写，则将标签转为html中同名元素；若为大写，react就去渲染对应的组件

*注意if语句、switch语句、声明变量属于语句，不是表达式，不能出现在{}中
```js
const count = 100
function getName () {
    return 'jack'
}
function App () {
    return (
        <div className="App">
            {/* 1. 使用引号传递字符串 */}
            {'this is message'}
            {/* 2. 使用JavaScript变量 */}
            {count}
            {/* 3. 函数调用和方法调用 */}
            {getName()}
            {new Date().getDate()}
            {/* 4. 使用JavaScript对象 */}
            <div style={{color:'red'}}>this is div</div>
        </div>
    )
}
```
**列表渲染**：`list.map`<br>
注意需要加上key(字符串或number id)，作用是React框架内部使用，提升性能的，不加的话控制器会报错
```js
const list = [
    {id: 1, name: 'Vue'},
    {id: 2, name: 'React'},
    {id: 3, name: 'Angular'}
]
function App () {
    return (
        <div className="App">
            <ul>
                {list.map(item => <li key={item.id}>{item.name}</li>)}
            </ul>
        </div>
    )
}
```
**条件渲染**：
1. 逻辑与运算符 *&&*

    `{flag && <span>this is span</span>}`<br>
    flag = true时显示this is span

2. 三元表达式 *?:*
    
    `{loading ? <span>loading</span> : <span>this is span</span>}`

3. 复杂情况 *自定义函数+if判断语句*
    ```js
    const type = 0
    function getType(){
        if(type === 0){
            return <div>零</div>
        }else if(type === 1){
            return <div>一</div>
        }else{
            return <div>其他</div>
        }
    }
    function App () {
        return (
            <div className="App">
                {getType()}
            </div>
        )
    }
    ```

# 虚拟DOM
**概念**：是一种用 JavaScript 对象来描述真实 DOM 结构的技术，用于提高渲染性能。更新 UI 时，先更新虚拟 DOM，再通过 diff 算法比较新旧虚拟 DOM，最终以最小的代价更新真实 DOM。与Vue虚拟DOM有一定区别

# React
## 事件绑定
1. 基础事件绑定

    *on + 事件名称 = {事件处理程序}*
    ```js
    function App () {
        const clickHandler = () => {
            console.log('按钮被点击')
        }
        return (
            <button onClick={clickHandler}></button>
        )
    }
    ```
2. 使用事件对象参数

    事件回调函数中 *设置形参e*<br>
    `const clickHandler = (e) => {console.log('按钮被点击')}`

3. 传递自定义参数

    事件绑定需要一个 *函数引用*
    ```js
    function App () {
        const clickHandler = (name) => {
            console.log('按钮被点击', name)
        }
        return (
            <button onClick={() => clickHandler('jack')}></button>
        )
    }
    ```

4. 同时传递事件对象和自定义参数
    ```js
    function App () {
        const clickHandler = (name, e) => {
            console.log('按钮被点击', name, e)
        }
        return (
            <button onClick={(e) => clickHandler('jack', e)}></button>
        )
    }
    ```

## 组件
```js
// 1.定义组件
function Button(){
    return <button></button>
}
function App () {
    return (
        <div className="APP">
            {/* 2. 渲染组件(一种自闭和，另一种成对标签) */}
            <Button />
            <Button></Button>
        </div>
    )
}
```

## useState
**概念**: 是一个React Hook(函数)，返回值是一个数组。允许向组件添加一个 *状态变量*，状态变量发生变化，组件视图UI也会跟着变化（*数据驱动视图*）

1. 修改简单数据类型状态 
    ```js
    // 例子：实现计数器按钮
    function App () {
        // 1.调用useState添加一个状态变量
        const [count, setCount] = useState(0)
        // 2.点击事件回调
        const handleClick = () => {
            setCount(count + 1)
        }
        return (
            <div>
                <button onClick={handleClick}>{count}</button>
            </div>
        )
    }
    ```
    其中[count, setCount]中，count是状态变量，setCount是修改状态变量的方法。useState(0)中的0是count的初始值<br>
    如果用count++直接修改，无法引发视图更新

2. 修改复杂数据类型（对象）状态
    ```js
    // 例子：实现点击按钮，按钮上的名字改变
    function App () {
        // 1.调用useState添加一个状态变量
        const [form, setForm] = useState({name: 'jack'})
        // 2.点击事件回调
        const changeForm = () => {
            setForm({
                ...form,
                name: 'john'
            })
        }
        return (
            <div>
                <button onClick={changeForm}>{form.name}</button>
            </div>
        )
    }
    ```
    其中...form是把form字段展开

## 基础样式控制
1. 行内样式（不推荐）
   
    `<div style={{color:'red', fontSize:'50px'}}>this is div</div>`<br>
    或<br>
    ```js
    const style = {
        color: 'red',
        fontSize: '50px'
    }
    function App () {
        return (
            <div>
                <span style={style}>this is span</span>
            </div>
        )
    }
    ```
    *注意，遇到多单词的样式需要写驼峰写法，例如fontSize
2. class类名控制

    ```js
    //导入css文件
    import './index.css'
    function App () {
        return (
            <div>
                {/* 绑定类名，注意是className不是class */}
                <span className='foo'>this is span</span>
            </div>
        )
    }
    ```
## classnames优化类名控制
**概念**：是一个简单的JS库，可以通过条件动态控制class类名的显示<br>
**例子**：条件为true情况标签绑定active类名，否则不绑定
```js
<span 
    key={item.type}
    onClick={() => handleTabChange(item.type)}
    className={`nav-item ${type === item.type && 'active'}`}>
    this is span
</span>
```
如上className的字符串拼接方式不够直观，也易错，就可以使用如下classnames优化<br>
1. `npm install classnames`<br>
2. 导入 `import classNames from 'classnames'`
3. 情况1：`className={classNames('nav-item', {active: type === item.type})}`其中nav-item为静态的类名，active: type === item.type为动态类名，active表示要控制的类名，type === item.type表示条件，true的话active类名显示  
情况2：`className={classNames('arraw', dateVisible && 'expend')}`当dateVisible时绑定类名arraw和expend，否则只绑定类名arraw

## 受控表单绑定
**概念**：使用React组件的状态(useState)控制表单的状态。state绑定到input的value属性，反过来，input把最新的value值设置给state<br>
**用法**：
```js
function App () {
    // 1. 声明一个react状态 - useState
    const [value, setValue] = useState('')
    return (
        <div>
            {/* 2. 通过value属性绑定react状态，并绑定onChange事件，通过参数e拿到输入框中最新的值，反向修改到react状态 */}
            <input
                value={value}
                onChange={(e) => setValue(e.target.value)}
                type = "text" />
        </div>
    )
}
```

## 获取DOM
**用法**：在React组件中获取/操作DOM，需要使用*useRef*钩子函数
```js
import { useRef } from "react"
function App () {
    // 1. useRef生成ref对象
    const inputRef = useRef(null)
    const showDom = () => {
        // 3. dom可用时(渲染完毕后dom生成后才可用)，ref.current获取dom
        console.dir(inputRef.current)
    }
    return (
        <div>
            {/* 2. ref绑定到dom标签上 */}
            <input type="text" ref={inputRef}/>
            <button onClick={showDom}>获取dom</button>
        </div>
    )
}
```

## forwardRef
**用法**：主要用于在组件之间传递refs，特别是在需要从一个父组件直接访问子组件或子组件中某个DOM元素的场景
```js
import {forwardRef, useRef} from "react"

const Son = forwardRef((props, ref) => {
  return <input type="text" ref={ref} />
})

function App(){
  const sonRef = useRef(null)
  const showRef = () => {
    console.log(sonRef)
    sonRef.current.focus()
  }
  return (
    <>
      <Son ref={sonRef}/>
      <button onClick={showRef}>focus</button>
    </>
  )
}

export default App
```

## useImperativeHandle
**概念**：通过ref暴露子组件中的方法

**用法**：例如现在父组件通过ref调用子组件内部的focus方法实现聚焦
```js
import {forwardRef, useImperativeHandle, useRef} from "react"

const Son = forwardRef((props, ref) => {
  const inputRef = useRef(null)
  const focusHandler = () => {
    inputRef.current.focus()
  }
  // 把聚焦方法暴露出去
  useImperativeHandle(ref, () => {
    return{
      focusHandler
    }
  })
  return <input type="text" ref={inputRef} />
})

function App(){
  const sonRef = useRef(null)
  const focusHandler = () => {
    console.log(sonRef.current)
    sonRef.current.focusHandler()
  }
  return (
    <>
      <Son ref={sonRef}/>
      <button onClick={focusHandler}>focus</button>
    </>
  )
}

export default App
```


## 组件通信
**概念**：就是 *组件之间的数据传递*，根据组件嵌套关系不同（父子通信、兄弟通信、跨层通信），有不同的通信方法。<br>
**用法**：
1. 父传子
    ```js
    //2. 子组件接受数据 props的参数
    function Son (props) {
        // props:对象里包含了父组件传递过来的所有数据
        return <div>this is son, {props.data}</div>
    }
    function App () {
        const name = 'this is app name'
        return (
            <div>
                {/* 1. 父组件传递数据 子组件标签上绑定属性 */}
                <Son data={name} />
            </div>
        )
    }
    ```
    *props说明：<br>
    (1) 可传递任意的数据（数字、字符串、布尔值、数组、对象、函数、JSX）
    ```js
    <Son 
        name={appName}
        age={20}
        isTrue={false}
        list={['Vue', 'React']}
        obj={{name:'jack'}}
        cb={() => console.log(123)}
        child={<span>this is span</span>}
    />
    ```

    (2) props是只读对象，子组件只能读取props中的数据，不能直接进行修改，父组件的数据只能由父组件修改

    *特殊的prop children:<br>
    场景：当我们把内容嵌套在子组件标签中时，父组件会自动在名为children的prop属性中接收该内容
    ```js
    <Son>
        <span>this is span</span>
    </Son>
    ```
    以上该情况，props中会自动存入`children: <span />`

2. 子传父
    ```js
    //核心：在子组件中调用父组件中的函数并传递实参
    function Son ({onGetSonMsg}) {
        const sonMsg = 'son msg'
        return (
            <div>
                this is Son
                <button onClick={() => onGetSonMsg(sonMsg)}>send</button>
            </div>
        )
    }

    function App () {
        const [msg, setMsg] = useState('')
        const getMsg = (msg) => {
            console.log(msg)
            setMsg(msg)
        }
        return (
            <div>
                this is App, {msg}
                <Son onGetSonMsg={getMsg}/>
            </div>
        )
    }
    ```

3. 兄弟传递

    **思路**：借助“状态提升”机制，通过父组件进行兄弟组件之间的数据传递。<br>
    **步骤**：(1) A组件先通过子传父的方式把数据传给父组件App (2) App拿到数据后通过父传子的方式再传递给B组件
    ```JS
    // A => App => B
    function A ({onGetAName}) {
        const name = 'A name'
        return (
            <div>
                this is A,
                <button onClick={() => onGetAName(name)}>send</button>
            </div>
        )
    }

    function B ({name}) {
        return (
            <div>
                this is B,
                {name}
            </div>
        )
    }

    function App () {
        const [name, setName] = useState('')
        const getAName = (name) => {
            console.log(name)
            setName(name)
        }
        return (
            <div>
                this is App
                <A onGetAName={getAName}/>
                <B name={name}/>
            </div>
        )
    }
    ```

4. 跨层级组件通信
    ```js
    // App => A => B
    // 1. createContext方法创建一个上下文对象
    const MsgContext = createContext()

    function A () {
        return (
            <div>
                this is A
                <B />
            </div>
        )
    }

    function B () {
        // 3. 在底层组件 通过useContext钩子函数使用数据
        const msg = useContext(MsgContext)
        return (
            <div>
                this is B,{msg}
            </div>
        )
    }

    function App () {
        const msg = 'App msg'
        return (
            <div>
                {/* 2. 在顶层组件 通过Provider组件提供数据 */}
                <MsgContext.Provider value={msg}>
                    this is App
                    <A />
                </MsgContext.Provider>
            </div>
        )
    }
    ```
    *注意：只要形成了底层和顶层的嵌套关系（例如同级子组件，远亲组件），就能使用context

## useEffect
**概念**：是一个React Hook函数，用于在React组件中创建不是由事件引起而是*由渲染本身引起的操作*，比如发送AJAX请求，更改DOM等。<br>
**语法**：`useEffect(() => {}, [])`

    第一个参数叫*副作用函数*，在函数内部可以放置要执行的操作
    第二个参数(可选参)叫*依赖项数组*，在数组里放置依赖项，不同依赖项会影响第一个参数函数的执行，当是一个空数组的时候，副作用函数只会在组件渲染完毕后执行一次

**依赖项参数说明**：
|依赖项|副作用函数执行时机|
|--|--|
|没有依赖项|组件初始渲染+组件更新时执行|
|空数组依赖|只在初始渲染时执行一次|
|添加特定依赖项|组件初始渲染+特定依赖项变化时执行|

```js
// 实现组件渲染后，从服务器获取列表数据并显示到页面
import {useEffect,useState} from "react"
const URL = 'http://geek.itheima.net/v1_0/channels'

function App () {
    //创建一个状态数据
    const [list, setList] = useState([])
    useEffect(() => {
        //额外的操作，获取列表
        async function getList(){
            const res = await fetch(URL)
            const jsonRes = await res.json()
            console.log(jsonRes)
            setList(jsonRes.data.channels)
        }
        getList()
    },[])
    return (
        <div>
            this is App
            <ul>
                {list.map(item => <li key={item.id}>{item.name}</li>)}
            </ul>
        </div>
    )
}

export default App
```
**清除副作用**：在useEffect中编写的由渲染本身引起的对接组件外部的操作，叫做*副作用操作*，例如在useEffect中开启了一个定时器，在组件卸载时把这个定时器清理掉（否则可能会引起内存泄漏），这个过程就是清理副作用。清除副作用的函数最常见的执行时机是在*组件卸载时自动执行*
```js
//在Son组件渲染时开启一个定时器，卸载时清除这个定时器
import {useEffect,useState} from "react"
function Son () {
    useEffect(() => {
        const timer = setInterval(() => {
            console.log('定时器执行中...')
        },1000)
        return () => {
            //清除副作用
            clearInterval(timer)
        }
    },[])
    return <div>Son</div>
}

function App () {
    //通过条件渲染模拟组件卸载
    const [show, setShow] = useState(true)
    return (
        <div>
            {show && <Son />}
            <button onClick={() => setShow(false)}>卸载</button>
        </div>
    )
}

export default App
```

## 自定义Hook函数
**概念**：自定义Hook函数是*以use打头的函数*，通过自定义Hook函数可以用来实现*逻辑的封装和复用*，在项目中通常放在src/hooks中

```js
//解决布尔切换的逻辑，组件耦合在一起，不方便复用的问题
import {useState} from "react"

//1.声明一个以use打头的函数
function useToggle () {
    //2.在函数体内封装可复用的逻辑
    const [value, setValue] = useState(true)
    const toggle = () => setValue(!value)

    //3.在组件中用到的状态或者回调return出去（以对象或者数组）
    return {
        value,
        toggle
    }
}

function App () {
    //4.在哪个组件中要用到这个逻辑，就执行这个函数，解构出来状态和回调进行使用
    const [value, toggle] = useToggle()
    return (
        <div>
            {value && <div>this is div</div>}
            <button onClick={toggle}>toggle</button>
        </div>
    )
}

export default App
```

## ReactHooks
**使用规则**：
1. 只能在组件中或者其他自定义Hook函数中调用
2. 只能在组件的顶层调用，不能嵌套在if、for、其他函数中

## useMemo
**概念**：React 的一个钩子函数，在组件每次重新渲染的时候*缓存计算的结果*，用于优化性能。它通过记忆函数的返回值，只有在依赖项变化时才重新计算，从而避免不必要的重复计算。（只有计算量大的时候会用）

**语法**：useMemo 接受两个参数。一个创建函数返回要记忆的值，一个依赖项数组，只有在这些依赖项发生变化时，创建函数才会重新执行。
```js
const result = useMemo(() => {
  // 计算过程
  return value;
}, [dependency1, dependency2, ...]);
```

## useReducer
**概念**：和useState作用相似，用来管理相对复杂的状态数据

<img src="https://i-blog.csdnimg.cn/direct/c1386251c7fb43b0a68fc6751ea6dda8.png#pic_center" width="600px" />

**基础用法**：
```js
import {useReducer} from "react"

// 1. 定义一个reducer函数（根据不同的action返回不同的新状态）
function reducer (state, action) {
    switch (action.type) {
        case 'INC':
            return state + 1
        case 'DEC':
            return state - 1
        case 'SET':
            return action.payload
        default:
            return state
    }
}

function App(){
    // 2. 在组件中调用useReducer，并传入reducer函数和状态的初始值
    const [state, dispatch] = useReducer(reducer, 0)
    return (
        <div>
            {/* 3. 事件发生时，通过dispatch函数分派一个action对象（通知reducer要返回哪个新状态并渲染UI） */}
            <button onClick={() => dispatch({type: 'DEC'})}>-</button>
            {state}
            <button onClick={() => dispatch({type: 'INC'})}>+</button>
            {/* 分派action时传参 */}
            <button onClick={() => dispatch({type: 'SET', payload: 100})}>update</button>
        </div>
    )
}

export default App
```


## reduce方法
**概念**：JavaScript 数组的一个常用方法，用于将数组中的每个元素按顺序处理并最终汇总为单个值。它适用于累加、求积、求和等操作。

**语法**：`arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])`其中callback 是一个函数，接受四个参数accumulator累计器、currentValue当前值、currentIndex当前索引（可选）以及array数组（可选）。另外initialValue（可选）作为第一次调用callback函数时第一个参数的值。

## React.memo
**概念**：存在react组件默认的渲染机制，只要父组件重新渲染子组件就会重新渲染，而React.memo允许组件在Props没有改变的情况下跳过渲染。

**基础用法**：
1. 用memo函数包裹组件
    ```js
    const MemoComponent = memo(function Son () {
        // ...
    })
    ```
2. 然后在父组件中return `<MemoComponent />`

**props的比较机制**：在使用memo缓存组件之后，react会对每一个prop使用Object.is比较新值和老值，返回true，表示没有变化
1. 传递一个简单类型的prop：prop变化时组件重新渲染
2. 传递一个引用类型的prop：比较的是新值和旧值得引用是否相等，当父组件得函数重新执行时，实际上形成的是新的数组引用。想要使得当父组件得函数重新执行时，不形成新数组引用需要使用useMemo组件渲染的过程中缓存一个值来保证引用稳定
    ```js
    const list = useMemo(() => {
        return [1, 2, 3]
    },[])
    ```

## useCallback
**概念**：在组件多次重新渲染的时候缓存函数。使用useCallback包裹函数后，函数可以保证在父组件重新渲染时保持引用稳定

<img src="https://i-blog.csdnimg.cn/direct/204ce79044bc47049ef8cb6cae3e9325.png#pic_center" width="600px" />

# 类组件基础结构
**概念**：就是通过js中的类来组织组件的代码
```js
import {Component} from "react"

class Counter extends Component {
  // 1.通过类属性state定义状态数据
  state = {
    count:0
  }
  // 2. 通过setState方法来修改状态数据
  setCount = () => {
    this.setState({
      count:this.state.count + 1
    })
  }
  // 3.通过render来写UI模板（JSX语法一致）
  render(){
    return <button onClick={this.setCount}>{this.state.count}</button>
  }
}

function App(){
  return (
    <>
      <Counter />
    </>
  )
}

export default App
```

## 类组件的生命周期函数
**概念**：组件从创建到销毁的各个阶段自动执行的函数就是生命周期函数
<img src="https://i-blog.csdnimg.cn/direct/84f5145b9b124ce19b2fb68b48951a08.png#pic_center" width="900px" />

## 类组件的组件通信
1. 父传子：通过prop绑定数据
    ```js
    class Son extends Component {
        render(){
            return <div>子组件 {this.props.msg}</div>
        }
    }

    class Parent extends Component {
        state = {
            msg: 'parent msg'
        }
        render(){
            return <div>父组件<Son msg={this.state.msg}/></div>
        }
    }

    function App(){
        return (
            <>
            <Parent />
            </>
        )
    }

    export default App
    ```
2. 子传父：通过prop绑定父组件中的函数，子组件调用
    ```js
    class Son extends Component {
        render(){
            return <>
            <div>子组件</div>
            <button onClick={() => this.props.onGetSonMsg('son数据')}>sendMsgToParent</button>
            </>
        }
    }

    class Parent extends Component {
        state = {}
        getSonMsg = (sonMsg) => {
            console.log(sonMsg)
        }
        render(){
            return <div>父组件<Son onGetSonMsg={this.getSonMsg} /></div>
        }
    }

    function App(){
        return (
            <>
            <Parent />
            </>
        )
    }

    export default App
    ```
3. 兄弟通信：状态提升，通过父组件做桥接


# Redux
**概念**: Redux是React最常用的*集中状态管理工具*，类似于Vue中的Pinia（Vuex），*可以独立于框架运行*。<br>
**作用**: 通过集中管理的方式管理应用的状态。

<img src="https://i-blog.csdnimg.cn/direct/6e4642fc8c5444b4abfc7bd43d7aaa30.png#pic_center" width="400px" />

**管理数据流程**: 

<img src="https://i-blog.csdnimg.cn/direct/d936eeb3e809494690dc46575d737889.png#pic_center" width="500px" />

1. state：一个对象，存放我们管理的数据状态
2. action：一个对象，用来描述怎么改数据
3. reducer：一个函数，根据action的描述生成一个新的state

## 在React中使用redux
**配套工具**: 
1. Redux Toolkit(RTK)：官方推荐编写Redux逻辑的方式，是一套工具的集合集，简化书写方式
2. react-redux：用来链接Redux和React组件的中间件

**配置基础环境**: 
1. `npx create-react-app 项目名` 使用CRA快速创建React项目
2. `npm i @reduxjs/toolkit react-redux` 安装配套工具
3. `npm run start` 启动项目

**store目录结构**:

![](https://i-blog.csdnimg.cn/direct/4eab75b3376d4ded8872d85271ee8245.png)
1. 通常集中状态管理的部分都会单独创建一个单独的store目录
2. 应用通常会有很多个子store模块，所以创建modules目录，在内部编写业务分类的子store
3. store中的入口文件index.js的作用是组合modules中所有的子模块，并导出store

**Redux调试**:浏览器下载devtools工具 

**案例1**:实现计数器

1. 创建：执行store模块中导出的actionCreater方法得到要提交的action对象

    <img src="https://i-blog.csdnimg.cn/direct/d21724fc682548029ecbfb4bc2b9bd7a.png#pic_center" width="500px" />

2. 根store组合子模块

    <img src="https://i-blog.csdnimg.cn/direct/24a32d13b76b4150908e1f04d385c402.png#pic_center" width="500px" />

3. 内置*Provider*组件通过store参数把创建好的store实例注入到应用中，链接正式建立

    <img src="https://i-blog.csdnimg.cn/direct/3a6b909b439f4e82a858844b2606d312.png#pic_center" width="500px" />

4. 使用：用钩子函数*useSelector*把store中的数据映射到组件中。修改：使用*useDispatch*来生成提交action对象的dispatch函数

    <img src="https://i-blog.csdnimg.cn/direct/b89e6ae7597442e1a5cd420d0efa2203.png#pic_center" width="500px" />

**案例2**:在案例1基础上提交action传参实现需求。在reducers的同步修改方法中添加action对象参数，在调用actionCreater的时候传递参数，参数会被传递到action对象*payload*属性上

<img src="https://i-blog.csdnimg.cn/direct/1ff02b8450714a75ab5201bc41e6acc9.png#pic_center" width="600px" />

**案例3**:实现异步操作

1. 创建store的写法保持不变，配置好同步修改状态的方法
    ```js
    const channelStore = createSlice({
        name: 'channel',
        initialState: {
            channelList: []
        },
        reducers: {
            setChannels (state, action) {
                state.channelList = action.payload
            }
        }
    })
    ```
2. 单独封装一个函数，在函数内部return一个新函数，在新函数中封装异步请求获取数据以及调用同步actionCreater传入异步数据生成一个action对象，并使用dispatch提交
    ```js
    // 异步请求部分
    const {setChannels} = channelStore.actions

    const fetchChannelist = () => {
        return async (dispatch) => {
            const res = await axios.get('http://...')
            dispatch(setChannels(res.data.data.channels))
        }
    }
    export {fetchChannelist}
    ```
3. 组件中dispatch写法保持不变
    ```js
    // 使用useEffect触发异步请求执行
    useEffect(() => {
        dispatch(fetchChannelList())
    },[dispatch])
    ```

# Redux Toolkit
**概念**：Redux 官方推荐的现代状态管理方案，适合中大型项目
1. `npm install @reduxjs/toolkit react-redux`
2. 项目结构
    ```
    src/
    ├── store/
    │   ├── index.js          // 创建store
    │   └── reducers/
    │       └── tabSlice.js   // 创建slice模块
    ```
3. 创建 Slice
    ```js
    // store/reducers/tabSlice.js
    import { createSlice } from '@reduxjs/toolkit';

    const tabSlice = createSlice({
    name: 'tab',
    initialState: {
        isCollapsed: false,
    },
    reducers: {
        collapseMenu: (state) => {
            state.isCollapsed = !state.isCollapsed;
        }
    }
    });

    export const { collapseMenu } = tabSlice.actions;
    export default tabSlice.reducer;
    ```
4. 创建 Store 并注册模块
    ```js
    // store/index.js
    import { configureStore } from '@reduxjs/toolkit';
    import tabReducer from './tabSlice';

    const store = configureStore({
        reducer: {
            tab: tabReducer
        }
    });

    export default store;
    ```
5. 在应用入口绑定 Provider
    ```js
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import './index.css';
    import App from './App';
    import reportWebVitals from './reportWebVitals';
    import { Provider } from 'react-redux';
    import store from './store';

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
        <React.StrictMode>
            <Provider store={store}>
                <App />
            </Provider>
        </React.StrictMode>
    );

    // If you want to start measuring performance in your app, pass a function
    // to log results (for example: reportWebVitals(console.log))
    // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
    reportWebVitals();
    ```
6. 在组件中使用 Redux
    - 读取 state
        ```js
            import { useSelector } from 'react-redux';
            const collapsed = useSelector((state) => state.tab.isCollapsed);
        ```
    - 派发 action
        ```js
        import { useDispatch } from 'react-redux';
        import { collapseMenu } from '../store/tabSlice';

        const dispatch = useDispatch();
        dispatch(collapseMenu());
        ```




# zustand
**概念**：极简的状态管理工具
1. 安装包`npm i zustand`
2. 创建store以及绑定store到组件
    ```js
    import {create} from 'zustand'

    // 创建store
    const useStore = create((set) => {
        return {
            // 状态数据
            count: 0,
            // 修改状态数据的方法
            inc: () => {
                set((state) => ({ count: state.count + 1 }))
            }
        }
    })

    // 绑定store到组件
    function App(){
        const {count, inc} = useStore()
        return (
            <>
            <button onClick={inc}>{count}</button>
            </>
        )
    }

    export default App
    ```
    *注意点：在创建store中，函数参数必须返回一个对象，对象内部编写状态数据和方法。另外，set是用来修改数据的专门方法，必须调用它来修改数据。set语法1：参数是函数，需要用到老数据的场景，例如如上代码中的`set((state) => ({ count: state.count + 1 }))`利用老数据进行计算；set语法2：参数直接是一个对象，例如`set({count:100})`

## zustand异步支持
**概念**:对于异步的支持不需要特殊的操作，直接在函数中编写异步逻辑，最后只需要调用set方法传入新状态即可
```js
const useStore = create((set) => {
  return {
    channelList: [],
    fetchGetList: async () => {
      const res = await fetch(URL)
      const jsonRes = await res.json()
      set({
        channelList: jsonRes.data.channels
      })
    }
  }
})
```

## zustand切片模式
**用法**:当单个store比较大的时候，可以采用切片模式进行模块拆分组合，类似于模块化
```js
import {create} from 'zustand'

// 1. 拆分子模块
const createCounterStore = (set) => {
  return {
    count: 0,
    inc: () => {
      set((state) => ({ count: state.count + 1 }))
    }
  }
}
const createChannelStore = (set) => {
  return {
    channelList: [],
    fetchGetList: async () => {
      const res = await fetch(URL)
      const jsonRes = await res.json()
      set({
        channelList: jsonRes.data.channels
      })
    }
  }
}
// 2. 组合
const useStore = create((...a) => {
  return {
    ...createCounterStore(...a),
    ...createChannelStore(...a)
  }
})

function App(){
  // 3. 组件使用
  const {count, inc, channelList, fetchGetList} = useStore()
  return (
    <>
      <button onClick={inc}>{count}</button>
    </>
  )
}

export default App
```


# ReactRouter
**步骤**:
1. 安装包:`npm i react-router-dom`
2. src下创建router文件夹，router下创建index.js
    ```js
    import { createBrowserRouter } from 'react-router-dom'

    // 1.创建router实例对象并且配置路由对应关系
    const router = createBrowserRouter([
        {
            path: '/',
            element: <Layout />
        },
        {
            path: '/login',
            element: <Login />
        }
    ])

    export default router
    ```
3. 在src/index.js中添加代码
    ```js
    import { RouterProvider } from 'react-router-dom'
    import router from './router'

    const root = ReactDOM.createRoot(document.getElementById('root'))
    root.render(
        <React.StrictMode>
            {/* 2.路由绑定 */}
            <RouterProvider router={router} />
        </React.StrictMode>
    )
    ```

## 路由导航类型
1. **声明式导航**:通过在模板中使用`<link to="/article">文章</link>`。通过给组件的to属性指定要跳转到路由path，组件会被渲染为浏览器支持的a链接，如果需要传参直接用字符串拼接方式拼接参数即可
2. **编程式导航**:通过*useNavigate*钩子得到导航方法，通过调用方法以命令式的形式进行路由跳转
    ```js
    import { useNavigate } from 'react-router-dom'

    const Login = () => {
        const navigate = useNavigate()
        return (
            <div>
                <button onClick={() => navigate('/article')}>跳转</button>
            </div>
        )
    }
    ```
## 路由导航传参
1. **searchParams传参**:

    (1) 传参
    `navigate('/article?id=1001&name=jack')`

    (2) 使用参数
    ```js
    const [params] = useSearchParams()
    let id = params.get('id')
    ```
2. **params传参**:

    (1) 传参
    `navigate('/article/1001/jack')`
    ```js
    {
        path:'/article/:id/:name',
        element:<Article />
    }
    ```

    (2) 使用参数
    ```js
    const [params] = useParams()
    let id = params.id
    ```

## 嵌套路由配置步骤
1. 使用`children`属性配置路由嵌套关系
    ```js
    {
        path: '/',
        element: <Layout />,
        children: [
            {
                path: 'board',
                element: <Board />,
            },
            {
                path: 'about',
                element: <About />,
            },
        ],
    },
    ```
2. 使用`<Outlet />`组件配置二级路由渲染位置
    ```js
    const Layout = () => {
        return (
            <div>
                <Link to="board">面板</Link>
                <Link to="about">关于</Link>
                {/* 二级路由出口 */}
                <Outlet />
            </div>
        )
    }
    ```

## 默认二级配置
当访问的是一级路由时，默认的二级路由组件可以得到渲染，只需要在二级路由的位置*去掉path，设置index属性为true*
```js
{
    path: '/',
    element: <Layout />,
    children: [
        {
            index: true,
            element: <Board />,
        },
        {
            path: 'about',
            element: <About />,
        },
    ],
},
```
```js
const Layout = () => {
    return (
        <div>
            <Link to="/">面板</Link>
            <Link to="about">关于</Link>
            {/* 二级路由出口 */}
            <Outlet />
        </div>
    )
}
```

## 404路由配置
**场景**:当浏览器输入url的路径在整个路由配置中都找不到对应的path，为了用户体验，可以使用404兜底组件进行渲染

**实现步骤**:
1. 准备一个NotFound组件
    ```js
    const NotFound = () => {
        //自定义模板
        return <div>this is NotFound</div>
    }

    export default NotFound
    ```
2. 在路由表数组的末尾，以*号作为路由path配置路由
    ```js
    {
        path: '*',
        element:<NotFound />
    }
    ```

## 路由模式
1. **history模式**：由createBrowerRouter创建
2. **hash模式**：由createHashRouter创建

|路由模式|url表现|底层原理|是否需要后端支持|
|--|--|--|--|
|history|url/login|history对象+pushState事件|需要|
|hash|url/#/login|监听hashChange事件|不需要|

# 项目
## 项目src下目录
|文件夹|作用|
|--|--|
|apis|接口|
|assets|静态资源|
|components|通用组件|
|pages|页面级组件|
|router|路由Router|
|store|Redux状态|
|utils|工具函数|
## 别名路径配置
1. **路径解析配置（webpack）**：使用craco插件，把@/解析为src/

    步骤1：安装craco。`npm i -D @craco/craco`<br>
    步骤2：项目根目录下创建配置文件*craco.config.js*<br>
    步骤3：配置文件中添加路径解析配置<br>
    ```js
    const path = require('path')

    module.exports = {
        // webpack配置
        webpack:{
            // 配置别名
            alias:{
                // 约定：使用@表示src文件所在路径
                '@':path.resolve(__dirname, 'src')
            }
        }
    }
    ```
    步骤4：包文件package.json中配置启动和打包命令
    ```json
    "scripts":{
        "start": "craco start",
        "build": "craco build"
    },
    ```

2. **路径联想配置（VsCode）**：VsCode在输入@/时，自动联想出来对应的src/下的子级目录

    步骤1：根目录下新增配置文件 - jsconfig.json<br>
    步骤2：添加路径提示配置
    ```json
    {
        "compilerOptions":{
            "baseUrl":"./",
            "paths":{
                "@/*":[
                    "src/*"
                ]
            }
        }
    }
    ```

## 数据mock
**概念**：在前后端分离的开发模式下，前端可以在没有实际后端接口的支持下先进行接口数据的模拟，进行正常的业务功能开发

**常见Mock方式**：
1. 前端直接写假数据：纯静态，没有服务
2. 自研Mock平台：成本太高
3. json-server等工具：有服务，成本低

## json-server实现数据Mock
**概念**：json-server是一个node包，可在30秒内获得零编码的完整的Mock服务

**实现步骤**：
1. 安装json-server。`npm i -D json-server`
2. 准备一个json文件
3. 添加启动命令`"server": "json-server ./server/data.json --port 8888"`
4. 访问接口进行测试

## antd-mobile主题定制
**定制方案**：
1. 全局定制：整个应用范围内的组件都生效

    步骤1：在项目src下创建theme.css

    步骤2：添加代码
    ```css
    :root:root{
        --adm-color-primary: #a062d4;
    }
    ```
    步骤3：在入口文件index.js中导入定制主题文件`import './theme.css'`

2. 局部定制：只在某些元素内部的组件生效

    步骤1：在项目src下创建theme.css

    步骤2：添加代码
    ```css
    .类名{
        --adm-color-primary: #a062d4;
    }
    ```
    步骤3：在入口文件index.js中导入定制主题文件`import './theme.css'`

## 统一封装请求
**概念**：整个项目中会发送很多网络请求，使用axios三方库做统一封装，方便统一管理和复用

**目录结构**：

<img src="https://i-blog.csdnimg.cn/direct/c420481cc3144a0c98b2cb1009e5e9b5.png#pic_center" width="180px" />

**步骤**：
1. 在utils/request.js中添加代码
    ```js
    import axios from "axios"

    const request = axios.create({
        // 根域名配置
        baseURL: 'http://...',
        // 超时时间
        timeout: 5000
    })

    // 请求拦截器：在请求发送前做拦截，插入一些自定义配置 [参数的处理]
    request.interceptors.request.use((config) => {
        return config
    },(error) => {
        return Promise.reject(error)
    })

    // 响应拦截器：在响应返回到客户端前做拦截，重点处理返回的数据
    request.interceptors.response.use((response) => {
        // 2xx范围内状态码都会触发该函数
        return response.data
    },(error) => {
        // 超出2xx范围内状态码都会触发该函数
        return Promise.reject(error)
    })

    export {request}
    ```
2. 在utils/index.js中添加代码
    ```js
    // 统一中转工具模块函数
    import {request} from './request'

    export {
        request
    }
    ```

## 登录
### 使用Redux管理token
**概念**：token作为一个用户的标识数据，需要在很多个模块中共享，Redux可以方便的解决状态共享问题

**步骤**：
1. Redux中编写获取Token的异步获取和同步修改
2. Login组件负责提交action并且把表单数据传递过来

### Token持久化
**解决的问题**：Redux是基于浏览器内存的存储方式，刷新时状态恢复为初始值，持久化就是防止刷新浏览器时丢失Token，用Redux+LocalStorage解决

**步骤**：
1. Redux和LocalStorage中都存一份
    ```js
    reducers:{
        setToken (state, action) {
            state.token = action.payload
            localStorage.setItem('token_key', action.payload)
        }
    }
    ```
2. 初始化token时判断，如果localStorage中有数据则用localStorage，没有数据则用空字符串
    ```js
    initialState:{
        token: localStorage.getItem('token_key') || ''
    }
    ```

### 封装Token的存取删方法
**封装原因**：对于Token的各类操作在项目多个模块中都会用到，为了共享复用可以封装成工具函数

**思想**：在utils/token.js中封装setToken、getToken和removeToken方法，供其他模块使用
```js
const TOKENKEY = 'token_key'
function setToken (token) {
    localStorage.setItem(TOKENKEY, token)
}
function getToken () {
    return localStorage.getItem(TOKENKEY)
}
function removeToken () {
    localStorage.removeItem(TOKENKEY)
}

export {
    setToken,
    getToken,
    removeToken
}
```
### Axios请求拦截器注入Token
**原因**：Token作为用户的一个标识数据，后端很多接口都会以它作为接口权限判断的依据，请求拦截器注入Token后，所有用到Axios实例的接口请求都自动携带了Token
```js
request.interceptors.request.use((config) => {
    // 操作config，注入token数据
    // 1. 获取到token
    const token = getToken()
    // 2. 按照后端的格式要求做token拼接
    if (token) {
        config.headers.Authorization = `Bearer ${token}`
    }
    return config
},(error) => {
    return Promise.reject(error)
})
```
### 使用Token做路由权限控制
**概念**：有些路由页面的内容信息比较敏感，如果用户没有经过登录获取到有效的token，是没有权限跳转的，*根据token的有无控制当前路由是否可以跳转*就是路由的权限控制

<img src="https://i-blog.csdnimg.cn/direct/0ce2175cf1694c859e42614961e90793.png#pic_center" width="500px" />

**实现步骤**：
1. 封装高阶组件src/components/AuthRoute.js
    ```js
    import {getToken} from '@/utils'
    import {Navigate} from 'react-router-dom'

    export function AuthRoute ({children}) {
        const token = getToken()
        if (token) {
            return <>{children}</>
        } else {
            return <Navigate to={'/login'} replace />
        }
    }
    ```
2. 配置路由
    ```js
    {
        path: "/",
        element: <AuthRoute><Layout /></AuthRoute>
    }
    ```
## 样式reset
**实现步骤**：
1. 样式初始化`npm install normalize.css`
2. 在src/index.js引入`import 'normalize.css'`
3. 在src/index.scss中设置html、body以及root高度都为100%
    ```scss
    html,
    body,
    #root {
        height: 100%;
    }
    ```
## Layout
### 根据当前路由路径高亮菜单
**效果描述**：页面在刷新时可以根据当前的路由路径让对应的左侧菜单高亮显示

**实现步骤**：
1. 获取当前url上的路由路径，要用到useLocation钩子函数
    ```js
    const location = useLocation()
    const selectedKey = location.pathname
    ```
2. 找到菜单组件负责高亮的属性，绑定当前的路由路径`selectedKeys={selectedKey}`

### 展示个人信息
**用户信息维护**：和Token令牌类似，用户的信息通常很有可能在多个组件中都需要共享使用，所以同样应该放到Redux中维护

**实现步骤**：
1. 使用Redux进行信息管理
2. Layout组件中提交action
3. Layout组件中完成渲染

### 退出登录
**实现步骤**：
1. 用户确认之后清除用户信息，包括token以及其他个人信息
    ```js
    reducers:{
        clearUserInfo (state) {
            state.token = ''
            state.userInfo = {}
            removeToken()
        }
    }
    ```
2. 跳转到登录页
    ```js
    const onConfirm = () => {
        dispatch(clearUserInfo())
        navigate('/login')
    }
    ```
### 处理Token失效
**Token失效**：为了用户安全和隐私考虑，在用户长时间未在网站中做任何操作且规定的失效时间到达后，当前的Token就会失效，失效后不能再作为用户令牌标识请求隐私数据

**前端如何判断Token失效**：通常在Token失效后再去请求接口，后端会返回401状态码，前端可以监控这个状态做后续的操作

**Token失效前端做什么**：在axios拦截中监控401状态码，清除失效Token，跳转到登录页
```js
request.interceptors.response.use((response) => {
    return response.data
},(error) => {
    console.dir(error)
    if(error.response.status === 401){
        removeToken()
        router.navigate('/login')
        window.location.reload()
    }
    return Promise.reject(error)
})
```
## API模块封装
**解决问题**：当前接口请求放在功能实现的位置，没有在固定的模块内维护，后期查找维护困难，把项目中所有接口按照业务模块*以函数的形式*统一封装到apis模块中

<img src="https://i-blog.csdnimg.cn/direct/ff3251250cdf4a379a0ba4decff5b486.png#pic_center" width="600px" />

**实现步骤**：在src/apis/user.js中放置用户相关所有请求
```js
import {request} from "@/utils"

// 登录请求
export function loginAPI(formData){
    return request({
        url:'/authorizations',
        method:'POST',
        data:formData
    })
}
```

## 项目打包和本地预览
1. **项目打包**：将项目中的源代码和资源文件进行处理，生成可在生产环境中运行的静态文件的过程。`npm run build`
2. **本地预览**：在本地通过静态服务器模拟生产服务器运行项目的过程。

    步骤1：安装本地服务包`npm i -g serve`

    步骤2：`serve -s build`

    步骤3：浏览器访问

## 配置路由懒加载
**概念**：指路由的JS资源只有在被访问时才会动态获取，优化项目首次打开的时间

**实现步骤**：
1. 在src/router/index.js中把路由修改为由React提供的*lazy函数*进行动态导入
    ```js
    import {lazy} from 'react'

    const Home = lazy(() => import('@/pages/Home'))
    ```
2. 使用react内置的*Suspense组件*，包裹路由中element选项对应的组件
    ```js
    {
        index:true,
        element: <Suspense fallback={'加载中'}><Home /></Suspense>
    }
    ```

## 包体积分析
**概念**：通过可视化的方式，直观体检项目中各种包打包之后的体积大小，方便做优化

**实现步骤**：
1. 安装包`npm i source-map-explorer`
2. 在package.json中配置如下命令指定要分析的js文件后，运行`npm run analyze`即可
    ```js
    "scripts":{
        "analyze":"source-map-explorer 'build/static/js/*.js'"
    }
    ```

## CDN优化
**概念**：CDN是一种内容分发网络服务，当用户请求网站内容时，由*离用户最近的服务器*将缓存的资源内容传递给用户

**哪些资源可以放到CDN服务器**：体积较大的非业务JS文件（非业务JS文件指的是不需要经常做变动，CDN不用频繁更新缓存的），比如react、react-dom

**项目中实现**：
1. 在craco.config.js中把需要做CDN缓存的文件排除在打包之外

<img src="https://i-blog.csdnimg.cn/direct/cff1438eb1bd4c2e8672ad89faa72fea.png#pic_center" width="600px" />

2. 在public/index.html中以CDN的方式重新引入资源

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/e86f02c0e10245d7b73da80559612c6d.png)

# React+TypeScript
基于Vite（一个框架无关的前端工具链）创建开发环境 `npm create vite@latest my-app -- --template react-ts`
## useState自动推导
**概念**：通常React会根据传入useState的默认值来自动推导类型，不需要显式标注类型，例如`const [value, toggle] = useState(false)`会自动推导出value和toggle类型都为boolean
## useState传递泛型参数
**概念**：useState本身是一个泛型函数，可以传入具体的自定义类型
```ts
type User = {
    name: string
    age: number
}
const [user, setUser] = useState<User>()
```
*注意：上面代码中 
1. 限制useState函数参数的初始值必须满足类型为 User | () => User
2. 限制setUser函数的参数必须满足类型为 User | () => User | undefined
3. user状态数据具备User类型相关的类型提示
## useState初始值为null
**概念**：当我们不知道状态的初始值是什么，将useState的初始值为null是常见的做法，可以通过*具体类型联合null*来做显式注解
```ts
type User = {
  name: string
  age: number
}

function App(){
  const [user, setUser] = useState<User | null>(null)

  const changeUser = () => {
    setUser(null)
    setUser({
      name: 'jack',
      age: 18,
    })
  }
  // 为了类型安全，可选链做类型守卫，只有user不为空值时才进行点运算
  return <>{user?.age}</>
}

export default App
```
## props与TypeScript—基本使用
**概念**：为组件prop添加类型，本质是给函数的参数做类型注解，可以使用type对象类型或者interface接口来做注解
```ts
// 方法1：使用type对象类型
type Props = {
  className: string
}
// 方法2：使用interface接口
interface Props {
  className: string
}

function Button(props: Props){
  const {className} = props
  return <button className={className}>click</button>
}

function App(){
  return (
    <>
      {/* Button组件只能传入名称为className的prop参数，类型为string并且必填 */}
      <Button className="test" />
    </>
  )
}

export default App
```
## props与TypeScript—为children添加类型
**概念**：children是一个比较特殊的prop，支持多种不同类型数据的传入，需要通过一个*内置的ReactNode类型*来做注解，注解后children可以是多种类型，包括React.ReactElement、string、number、React.ReactFragment、React.ReactPortal、boolean、null和undefined
```ts
type Props = {
  className: string
  children: React.ReactNode
}

function Button(props: Props){
  const {className, children} = props
  return <button className={className}>{children}</button>
}

function App(){
  return (
    <>
      <Button className="test">
        <span>span</span>
      </Button>
    </>
  )
}

export default App
```
## props与TypeScript—为事件prop添加类型
**概念**：组件经常执行类型为函数的prop实现子传父，这类prop重点在于函数参数类型的注解
```ts
type Props = {
  onGetMsg?:(msg: string) => void
}

function Son(props: Props){
  const {onGetMsg} = props
  const clickHandler = () => {
    onGetMsg?.('this is msg')
  }
  return <button onClick={clickHandler}>sendMsg</button>
}

function App(){
  const getMsgHandler = (msg: string) => {
    console.log(msg)
  }
  return (
    <>
      {/* 绑定prop时如果绑定内联函数直接可以判断出参数类型，否则需要单独注解匹配的参数类型 */}
      <Son onGetMsg={(msg) => console.log(msg)} />
      <Son onGetMsg={getMsgHandler} />
    </>
  )
}

export default App
```
*注意：在组件内部调用时需要遵守类型的约束，参数传递需要满足要求
## useRef与TypeScript—获取dom
**概念**：获取dom的场景，可以直接把要获取的dom元素的类型当成泛型参数传递给useRef，可以推导出.current属性的类型
```ts
function App(){
  const domRef = useRef<HTMLInputElement>(null)
  useEffect(() => {
    domRef.current?.focus()
  }, [])
  return (
    <>
      <input ref={domRef} />
    </>
  )
}
```
## useRef与TypeScript—引用稳定的存储器
**概念**：把useRef当成引用稳定的存储器使用的场景就可以通过*泛型传入联合类型*来做，比如下面的定时器场景
```ts
function App(){
  const timerId = useRef<number | undefined>(undefined)
  useEffect(() => {
    timerId.current = setInterval(() => {
      console.log('123')
    }, 1000)
    return () => clearInterval(timerId.current)
  }, [])
  return <>this is div</>
}
```
## 封装API模块—axios和ts的配合使用
**场景**：axios提供了request泛型方法，方便我们传入类型参数推导出接口返回值的类型

<img src="https://i-blog.csdnimg.cn/direct/fe234a8319ee4051a979de854a2f00a3.png#pic_center" width="900px" />

**用法**：
1. 在src/apis/shared.ts中，根据接口文档创建一个通用的泛型接口类型（多个接口返回值的结构是相似的）(如上图绿框)
2. 在src/apis/list.ts中，根据接口文档创建特有的接口数据类型（每个接口有自己特殊的数据格式）(如上图蓝框)
3. 在src/apis/list.ts中，组合1和2的类型，得到最终传给request泛型的参数类型
    ```ts
    import { http } from '@/utils'

    export function fetchChannelAPI(){
    return http.request<ResType<ChannelRes>>({
        url: '/channels',
    })
    }
    ```
    若接口存在参数可以这样操作
    ```ts
    type ReqParams = {
    channel_id: string
    timestamp: string
    }

    export function fetchListAPI(params: ReqParams){
    return http.request<ResType<ListRes>>({
        url: '/articles',
        params,
    })
    }
    ```
## 自定义hook函数优化（可选）
**场景**：当前状态数据的各种操作逻辑和组件渲染是写在一起的，可以采用自定义hook封装的方式*让逻辑和渲染相分离*

**实现步骤**：
1. 把和组件例如Tabs相关的响应式数据状态以及操作数据的方法放到hook函数中
<img src="https://i-blog.csdnimg.cn/direct/93c16d9be4d842928f53336b1ab32505.png#pic_center" width="800px" />
2. 组件中调用hook函数，消费其返回的状态和方法
<img src="https://i-blog.csdnimg.cn/direct/704efe51bb5247a19e7dcf99c5fefa98.png#pic_center" width="800px" />
