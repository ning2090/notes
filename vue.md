# Vue
**概念**：渐进式JavaScript框架。基于标准HTML、CSS和JavaScript构建，提供了一套声明式的、组件化的编程模型。易学易用，性能出色，适用场景丰富的Web前端框架

## MVVM模型
1. 模型Model：对应data中的数据
2. 视图View：模板
3. 视图模型ViewModel：Vue实例对象

<img src="https://i-blog.csdnimg.cn/direct/f4b9596d35b44e3e9d253782b52e86e3.png#pic_center" width="600">

## 虚拟DOM
**概念**：是一种在内存中构建和操作的 JavaScript 对象树，用来描述真实 DOM 的结构信息，是为了解决浏览器性能问题引入的概念。其中的diff算法 是用来高效对比新旧虚拟DOM（Virtual DOM），找出最小差异并更新真实DOM的机制。

## 数据代理
**概念**：通过vm对象来代理data对象中属性的操作(读/写)，从而方便操作data中的数据<br>
**基本原理**：
1. 通过Object.defineProperty()把data对象中所有属性添加到vm上
2. 为每一个添加到vm上的属性，都指定一个getter/setter
3. 在getter/setter内部去操作(读/写)data中对应的属性

<img src="https://i-blog.csdnimg.cn/direct/277599c6b1484af3a5be037dec3cea08.png#pic_center" width="700">

## Vue监视数据的原理
**概念**：Vue会监视data中所有层次的数据<br>
>**监测对象中的数据**：通过setter实现监视，且在new Vue时就传入要监测的数据
>1. 对象中后追加的属性，Vue默认不做响应式处理
>2. 如需给后追加的属性做响应式，使用`Vue.set(target, propertyName/index, value)` 或 `vm.$set(target, propertyName/index, value)`，但是注意这两种方法不能给vm或vm的根数据对象(data、_data)添加属性

>**监测数组中的数据**：通过包裹数组更新元素(如push、pop等)的方法实现，本质是做了如下两件事
>1. 调用原生对应的方法对数组进行更新
>2. 重新解析模板，进而更新页面

## Vue数据劫持
**概念**：是Vue实现响应式的核心机制，它通过拦截对象属性的读写操作，使得数据变化时能自动触发视图更新。（Vue2用 Object.defineProperty，Vue3用 Proxy）

## Vue API 风格
1. 选项式 API
2. 组合式 API

## 创建项目
**命令**：`npm init vue@latest`

<img src="https://i-blog.csdnimg.cn/direct/1a6c18a3dd7c412dbd7d63f35efa05c7.png#pic_center" width="600">

*注意：<br>
项目名字不要大写<br>
`npm install` 可以换成 `cnpm install`，意为镜像，会安装的更快

## 项目目录结构
<img src="https://i-blog.csdnimg.cn/direct/8b5ee31f64284024985d6555129e93d0.png#pic_center" width="350">

- `main.js`：项目的JavaScript入口，初始化Vue实例并挂载到DOM
- `App.vue` ：根组件文件，承载整个应用的组件结构和公共布局
- `index.html`：静态页面模板，提供Vue挂载的DOM容器节点（如`<div id="app">`）

## el的两种写法
```js
const v = new Vue({
    // el:'#root', // 第一种写法
    data:{
        name:'wjn'
    }
})
v.$mount('#root') // 第二种写法
```

## data的两种写法
```js
const vm = new Vue({
    el:'#root', 
    // 第一种写法：对象式
    data:{
        name:'wjn'
    }
    // 第二种写法：函数式 (推荐，上一种在用到组件时会报错)
    data(){
        return{
            name:'wjn'
        }
    }
})
```


## 模板语法
**概念**：Vue使用一种基于HTML的模板语法，使我们能够声明式地将其组件实例的数据绑定到呈现的DOM上。所有的Vue模板都是语法层面合法的HTML，可以被符合规范的浏览器和HTML解析器解析

### 文本插值
**概念**：最基本的数据绑定形式是文本插值，使用“Mustache”语法(即双大括号)<br>
每个绑定仅支持单一表达式。
```html
<template>
    <p>{{ number + 1 }}</p>
    <p>{{ ok ? 'YES' : 'NO' }}</p>
    <p>{{ msg.split('').reverse().join('') }}</p>
</template>

<script>
export default{
    data(){
        return{
            number: 10,
            ok: true,
            msg: "大家好"
        }
    }
}
</script>
```

### 原始HTML
**概念**：双大括号会将数据插值为纯文本，而不是HTML。若想插入HTML，须使用 `v-html` 指令
```html
<template>
    <p>{{ rawHtml }}</p>
    <p v-html="rawHtml"></p>
</template>

<script>
export default{
    data(){
        return{
            rawHtml: "<a href="...">程序员</a>"
        }
    }
}
</script>
```

## 属性绑定
**概念**：双大括号不能在HTML attributes中使用，想要响应式地绑定一个attribute，使用 `v-bind` 指令<br>
因为常用，所以通常简写`:`
```html
<template>
    <div :id="dynamicId" :class="dynamicClass">AppID</div>
    <button :disabled="isDisabled">Button</button>
</template>

<script>
export default{
    data(){
        return{
            dynamicId:"appid",
            dynamicClass:"appclass",
            isDisabled:true
        }
    }
}
</script>
```
**动态绑定多个值**：
```html
<template>
    <div v-bind="objectOfAttrs">AppID</div>
</template>

<script>
export default{
    data(){
        return{
            objectOfAttrs:{
                id:"appid",
                class:"appclass"
            }
        }
    }
}
</script>
```

## 条件渲染
- `v-if`：这块内容只有在指令的表达式返回真值时才被渲染。当这块内容中为真值时，就不会再去判断v-else和v-else-if里的内容
- `v-else`
    ```html
    <template>
        <div v-if="flag">hi</div>
        <div v-else>hello</div>
    </template>

    <script>
    export default{
        data(){
            return{
                flag:ture
            }
        }
    }
    </script>
    ```
- `v-else-if`
    ```html
    <template>
        <div v-if="type === 'A'">A</div>
        <div v-else-if="type === 'B'">B</div>
        <div v-else-if="type === 'C'">C</div>
        <div v-else>D</div>
    </template>

    <script>
    export default{
        data(){
            return{
                type:"B"
            }
        }
    }
    </script>
    ```
- `v-show`
    ```html
    <template>
        <div v-show="flag">hi</div>
    </template>

    <script>
    export default{
        data(){
            return{
                flag:ture
            }
        }
    }
    </script>
    ```
**v-if和v-show对比**：<br>
*v-if* 是真实的按条件渲染，确保在切换时条件区块内的事件监听器和子组件都会被销毁与重建。但也是惰性的，若初次渲染时为false，则不会做任何事，只有首次为true时才被渲染。<br>
*v-show* 是无论初始条件如何，都会被渲染，只有CSS的display属性会被切换。<br>
总结：v-if有更高的切换开销，而v-show有更高的初始渲染开销。因此，*若频繁切换使用v-show更合适*

## 列表渲染
**概念**：使用 `v-for` 指令基于一个数组来渲染一个列表，值使用item in items形式的特殊语法，也可以把in改成of<br>
**通过key管理状态**：当数据项顺序改变时，Vue不会随之移动DOM元素顺序，而是就地更新每个元素，确保在原本指定索引位置上渲染，为元素对应的块提供一个唯一的key属性以便它可以追踪每个节点的标识，从而重用和重新排序现有的元素。<br>
key绑定的值期望是一个基础类型的值，如字符串或number类型<br>
尽量不使用index作为key的值，因为要确保每条数据的唯一索引不会发生变化
```html
<template>
    <div v-for="(name,index) in names" :key="index">{{ name }}-{{ index }}</div>
</template>

<script>
export default{
    data(){
        return{
            names:["w","j","n"]
        }
    }
}
</script>
```
**复杂数据**：如网络请求，也就是JSON格式
```html
<template>
    <div v-for="item in result" :key="item.id">
        <p>{{ item.title }}</p>
        <img :src="item.avator" alt="">
    </div>
</template>

<script>
export default{
    data(){
        return{
            result:[
                {
                    "id":1,
                    "title":"hi",
                    "avator":"..."
                },
                {
                    ...
                }
            ]
        }
    }
}
</script>
```
**遍历对象**：
```html
<template>
    <div v-for="(value,key,index) of userInfo">{{ value }}-{{ key }}-{{ index }}</div>
</template>

<script>
export default{
    data(){
        return{
            userInfo:{
                name:"w",
                age:20
            }
        }
    }
}
</script>
```

## 事件处理
**概念**：使用 `v-on` 指令(简写为 `@` )来监听DOM事件，并在事件触发时执行对应的JavaScript<br>
**用法**：`v-on:click="methodName"` 或 `@click="handler"`<br>
**事件处理器**：
- 内联事件处理器：事件被触发时执行的内联JavaScript语句(与onclick类似)
    ```html
    <template>
        <button @click="count++">Add</button>
        <p>{{ count }}</p>
    </template>

    <script>
    export default{
        data(){
            return{
                count:0
            }
        }
    }
    </script>
    ```
- 方法事件处理器：一个指向组件上定义的方法的属性名或是路径
    ```html
    <template>
        <button @click="addCount">Add</button>
        <p>{{ count }}</p>
    </template>

    <script>
    export default{
        data(){
            return{
                count:0
            }
        },
        methods:{
            addCount(e){
                e.target.innerHTML = "Add" + this.count
                this.count+=1
            }
        }
    }
    </script>
    ```

**传递参数过程中获取event**：
```html
<template>
    <div @click="getName(item,$event)" v-for="(item,index) in names" :key="index">{{ item }}</div>
</template>

<script>
export default{
    data(){
        return{
            names:["w","j","n"]
        }
    },
    methods:{
        getName(name,e){
            console.log(name,e);
        }
    }
}
</script>
```
**事件修饰符**：
- `.stop`：阻止事件冒泡。相当于event.stopPropagation()
    ```html
    <!-- 实现点击P后只打印P -->
    <template>
        <div @click.stop="clickDiv">
            <p @click.stop="clickP">P</p>
        </div>
    </template>

    <script>
    export default{
        data(){
            return{

            }
        },
        methods:{
            clickDiv(){
                console.log("DIV");
            },
            clickP(){
                console.log("P");
            }
        }
    }
    </script>
    ```
- `.prevent`：阻止默认事件。相当于event.preventDefault()
    ```html
    <template>
        <a @click.prevent="clickHandle" href="...">链接</a>
    </template>

    <script>
    export default{
        data(){
            return{

            }
        },
        methods:{
            clickHandle(){
                console.log(111);
            }
        }
    }
    </script>
    ```
- `.once`：事件只触发一次
- 等等

**键盘事件**：
1. 按键别名
    - `.enter`：回车
        ```html
        <template>
            <input type="text" @keyup.enter="showInfo">
        </template>

        <script>
        export default{
            data(){
                return{

                }
            },
            methods:{
                showInfo(e){
                    console.log(e.target.value);
                }
            }
        }
        </script>
        ```
    - `.delete`：删除
    - `.esc`：退出
    - `.space`：空格
    - `.tab`：换行 (特殊，须配合keydown使用)
    - `.up`：上
    - `.down`：下
    - `.left`：左
    - `.right`：右
2. Vue未提供别名的按键，可以使用按键原始key值去绑定，两个单词组成的词注意要转为kebab-case形式
3. 系统修饰键：`ctrl`、`alt`、`shift`、`meta`
    - 配合keyup使用：按下修饰键的同时按下其他键，随后释放其他键，事件才被触发
    - 配合keydown使用：正常触发事件
4. 使用keyCode去指定具体的按键(不推荐)
5. `Vue.config.keyCodes.自定义键名 = 键码`：定制按键别名

## 数组变化侦测
**概念**：Vue能够侦听响应式数组的变更办法，并在它们被调用时触发相关的更新<br>
**方法**：
- push()
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()

```html
<template>
    <button @click="addListHandle">添加数据</button>
    <ul>
        <li v-for="(item,index) in names" :key="index">{{ item }}</li>
    </ul>
</template>

<script>
export default{
    data(){
        return{
            names:["w","j","n"]
        }
    },
    methods:{
        addListHandle(){
            this.names.push("y")
            // 像concat、filter、slice因为返回新数组不更改原数组，无法触发UI更新，所以可以以下使得触发更新
            // this.names = this.names.concat(["y"])
        }
    }
}
</script>
```

## 计算属性
**概念**：来描述依赖响应式状态的复杂逻辑。或者可以理解为要用的属性不存在，要通过已有属性计算得来
**原理**：底层借助了Object.defineProperty方法提供的getter和setter。其中get函数在初次读取时会执行一次，当依赖数据发生变化时再次调用。set函数是计算属性要被修改时使用。
```html
<template>
    <h3>{{ baizhan.name }}</h3>
    <p>{{ baizhanContent }}</p>
    <p>{{ baizhanContents() }}</p>
</template>

<script>
export default{
    data(){
        return{
            baizhan:{
                name:"wjn",
                content:["前端", "python"]
            }
        }
    },
    // 计算属性
    computed:{
        // 完整写法
        baizhanContent:{
            get(){
                return this.baizhan.content.length > 0 ? 'Yes' : 'No'
            },
            set(value){
                console.log(value)
            }
        }
        // 如果不需要set函数可以使用以下简写
        baizhanContent(){
            return this.baizhan.content.length > 0 ? 'Yes' : 'No'
        }
    },
    // 函数或方法
    methods:{
        baizhanContents(){
            return this.baizhan.content.length > 0 ? 'Yes' : 'No'
        }
    }
}
</script>
```
**区别**：<br>
*计算属性*：计算属性值会基于其响应式依赖被缓存。一个计算属性仅会在其响应式依赖更新时才重新计算。就是在template中多次使用但是只会计算一次，而方法每用一次就得调用一次<br>
*方法*：方法调用总是会再重渲染发生时再次执行函数

## Class绑定
**概念**：数据绑定的常见需求场景是操纵元素的CSS class列表，Vue专门为class的v-bind用法提供了特殊的功能增强，除了字符串外，表达式的值也可以是对象或数组
```html
<!-- 此情况下，isActive:true字体红色，false则不为红 -->
<template>
    <p :class="{ 'active':isActive, 'text-danger':hasError }">样式绑定1</p>
    <p :class="classObject">样式绑定2</p>
    <p :class="[arrActive, arrHasError]">样式绑定3</p>
    <p :class="[isActive ? 'active text-danger' : '']">样式绑定4</p>
    <!-- 数组和对象嵌套过程中，只能是数组嵌套对象，不能反其道而行 -->
    <p :class="[isActive ? 'active' : '',{'text-danger':hasError}]">样式绑定5</p>
</template>

<script>
export default{
    data(){
        return{
            isActive:true,
            hasError:false,
            classObject:{
                'active':true,
                'text-danger':false
            },
            arrActive:"active",
            arrHasError:"text-danger"
        }
    }
}
</script>

<style>
.active{
    color:red;
}
</style>
```

## Style绑定
```html
<template>
    <p :style="{color:activeColor,fontSize:fontSize + 'px'}">Style绑定1</p>
    <p :style="styleObject">Style绑定2</p>
    <p :style="[styleObject]">Style绑定3</p>
</template>

<script>
export default{
    data(){
        return{
            activeColor:"green",
            fontSize:30,
            styleObject:{
                color:"red",
                fontSize:"30px"
            }
        }
    }
}
</script>
```

## 侦听器
**概念**：当监听属性变化时，回调函数自动调用，进行相关操作
```html
<template>
    <p>{{ message }}</p>
    <button @click="updateHandle">修改数据</button>
</template>

<script>
export default{
    data(){
        return{
            message:"hello"
        }
    },
    methods:{
        updateHandle(){
            this.message = "world"
        }
    },
    watch:{
        // 完整写法
        message:{
            immediate:true, // 初始时让handler调用一下
            deep:true, // 深度监视，用于监测对象内部多层值改变
            handler(newValue,oldValue){
                console.log(newValue,oldValue);
            }
        }
        // 如果不需要immediate和deep可以如下简写
        message(newValue,oldValue){
            // 数据发生变化，自动执行的函数
            console.log(newValue,oldValue);
        }
    }
}
</script>
```

## 表单输入绑定
**方法**：`v-model`<br>
**修饰符**：
- .lazy：默认情况，v-model会在每次input事件后更新数据，添加lazy可以改为在每次change事件后更新数据
- .number：将输入的内容自动转为数字类型
- .trim：自动去除输入的首尾空格

```html
<template>
    <form>
        <!-- 实现输入即获取 -->
        <input type="text" v-model="userInfo.message">
        <p>{{ message }}</p>
        <!-- 年龄输入框 -->
        年龄<input type="number" v-model.number="userInfo.age">
        <!-- 单选框 -->
        男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
        女<input type="radio" name="sex" v-model="userInfo.sex" value="female">
        <!-- 复选框 -->
        学习<input type="checkbox" v-model="userInfo.hobby" value="study"> 
        吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat"> 
        <!-- 下拉菜单 -->
        <select v-model="userInfo.city">
            <option value="jiaxing">嘉兴</option>
            <option value="hangzhou">杭州</option>
        </select>
        <!-- 文本域 -->
        <textarea v-model.lazy="userInfo.other"></textarea>
        <!-- 同意条款框。没有设置input的value属性，收集的就是checked，勾选为ture，不勾选为false -->
        <input type="checkbox" v-model="userInfo.agree">阅读并接受条款
    </form>
</template>

<script>
export default{
    data(){
        return{
            userInfo:[
                message:"",
                age:null,
                sex:"female",
                hobby:[],
                city:"",
                other:"",
                agree:""
            ]
        }
    }
}
</script>
```

vue中有两种数据绑定方式：
1. 单向绑定v-bind：数据只能从data流向页面
2. 双向绑定v-model：数据不仅能从data流向页面，还能从页面流向data。一般应用在表单类元素(输入类元素)上。v-model:value可以简写成v-model，因为v-model默认收集的就是value值

## 模板引用：获取DOM
**方法**：`ref` (没有特别需求，不要操作DOM)
```html
<template>
    <div ref="container" class="container">{{ content }}</div>
    <input type="text" ref="username">
    <button @click="getElementHandle">获取元素</button>
</template>

<script>
export default{
    data(){
        return{
            content:"内容"
        }
    },
    methods:{
        getElementHandle(){
            this.$refs.container.innerHTML = "hi";
            console.log(this.$refs.username.value);
        }
    }
}
</script>
```

## 组件组成
**模块与组件的区别**：模块是向外提供特定功能的js程序，一般就是一个js文件；组件是用来实现局部功能效果的代码集合(html/css/js...)<br>
**优势**：可复用性<br>
**Vue实例和组件实例**：为的是让组件实例对象vc可以访问到Vue原型上的属性和方法

<img src="https://i-blog.csdnimg.cn/direct/1388a67c0b6348c3880531194c56f64b.png#pic_center" width="800">

**组件注册**：组件在使用前需先被注册，这样Vue才能在渲染模板时找到其对应的实现
- 全局注册 (虽然方便但项目中的依赖关系没那么明确；全局注册但没有使用的组件会被一起生产打包，使得文件过大)
    ```js
    <!-- 在main.js中写入以下代码后，在其他.vue文件中就可直接`<Header />`引入 -->
    import {createApp} from 'vue'
    import App from './App.vue'
    import Header from "./pages/Header.vue"

    const app = createApp(App)

    <!-- 在这中间写组件的注册 -->
    app.component("Header",Header)

    app.mount('#app')
    ```
- 局部注册
    ```html
    <template>
        <!-- 3. 显示组件 -->
        <MyComponent />
        <my-component />
    </template>

    <script>
        // 1. 引入组件
        import MyComponent from "./components/MyComponent.vue"
        export default{
            // 2. 注入组件
            components:{
                MyComponent
            }
        }
    </script>

    <!-- scoped让当前样式只在当前组件中生效。如果有lang="xxx"，指定样式语言类型，如less，默认是css -->
    <style scoped>
    </style>
    ```

## 组件传递数据
### 父传子
**方法**：`props` 传递数据是只读的，不能修改父元素传递过来的数据(可以通过在子组件data中重新定义一个变量，把传递的数据放进去再进行修改)
- 静态数据传递
    ```html
    <template>
        <h3>Parent</h3>
        <Child title="Parent数据" demo="测试"/>
    </template>

    <script>
    import Child from "./Child.vue"
    export default{
        data(){
            return{
            }
        },
        components:{
            Child
        }
    }
    </script>
    ```
    ```html
    <template>
        <h3>Child</h3>
        <p>{{ title }}</p>
        <p>{{ demo }}</p>
    </template>

    <script>
    export default{
        data(){
            return{
            }
        },
        props:["title","demo"]
    }
    </script>
    ```
- 动态数据传递
    ```html
    <template>
        <h3>Parent</h3>
        <Child :title="message" />
    </template>

    <script>
    import Child from "./Child.vue"
    export default{
        data(){
            return{
                message:"Parent数据"
            }
        },
        components:{
            Child
        }
    }
    </script>
    ```
    ```html
    <template>
        <h3>Child</h3>
        <p>{{ title }}</p>
    </template>

    <script>
    export default{
        data(){
            return{
            }
        },
        props:["title"]
    }
    </script>
    ```
**数据类型**：任何类型
```html
<template>
    <h3>Parent</h3>
    <Child :title="message" :age="age" :names="names" :userInfo="userInfo"/>
</template>

<script>
import Child from "./Child.vue"
export default{
    data(){
        return{
            message:"Parent数据",
            age:18,
            name:["w","j","n"],
            userInfo:{
                name:"wjn",
                age:18
            }
        }
    },
    components:{
        Child
    }
}
</script>
```
```html
<template>
    <h3>Child</h3>
    <p>{{ title }}</p>
    <p>{{ age }}</p>
    <ul>
        <li v-for="(item,index) of names">{{ item }}</li>
    </ul>
    <p>{{ userInfo.name }}</p>
    <p>{{ userInfo.age }}</p>
</template>

<script>
export default{
    data(){
        return{
        }
    },
    props:["title","age","names","userInfo"]
}
</script>
```
**数据校验**：常用的包括`type`、`required`和`default`。如type不符合，数据仍能显示，但在console会发生警告
```js
props:{
    title:{
        type:[String,Number,Array,Object],
        required:ture
    },
    // 数字和字符串可以直接default，但数组和对象必须通过工厂函数返回默认值
    age:{
        type:Number,
        default:0
    },
    names:{
        type:Array,
        default(){
            return ["空"]
        }
    }
}
```

### 子传父
**方法**：`$emit` 触发自定义事件
```html
<template>
    <h3>Child</h3>
    <button @click="clickEventHandle">传递数据</button>
</template>

<script>
export default{
    data(){
        return{
            msg:"Child数据"
        }
    },
    methods:{
        clickEventHandle(){
            this.$emit("someEvent",this.msg)
        }
    }
}
</script>
```
```html
<template>
    <h3>Parent</h3>
    <!-- 当Child触发someEvent自定义事件，Parent就触发getHandle事件，这两个事件名可以一样 -->
    <Child @someEvent="getHandle"/>
    <p>{{ message }}</p>
</template>

<script>
import Child from "./Child.vue"
export default{
    data(){
        return{
            message:""
        }
    },
    components:{
        Child
    },
    methods:{
        getHandle(data){
            this.message = data;
        }
    }
}
</script>
```

**配合v-model使用**：
```html
<template>
    <h3>Child</h3>
    搜索：<input type="text" v-model="search">
</template>

<script>
export default{
    data(){
        return{
            search:""
        }
    },
    watch:{
        search(newValue, oldValue){
            this.$emit("searchEvent",newValue)
        }
    }
}
</script>
```
```html
<template>
    <h3>Parent</h3>
    <Child @searchEvent="getSearch"/>
    <p>搜索内容：{{ search }}</p>
</template>

<script>
import Child from "./Child.vue"
export default{
    data(){
        return{
            search:""
        }
    },
    components:{
        Child
    },
    methods:{
        getSearch(data){
            this.search = data;
        }
    }
}
</script>
```

**props实现子传父（通过传递函数）**：
```html
<template>
    <h3>Child</h3>
    <p>{{ onEvent('传递数据') }}</p>
</template>

<script>
export default{
    data(){
        return{

        }
    },
    props:{
        onEvent:Function
    }
}
</script>
```
```html
<template>
    <h3>Parent</h3>
    <Child :onEvent="dataFn"/>
    <p>{{ message }}</p>
</template>

<script>
import Child from "./Child.vue"
export default{
    data(){
        return{
            message:""
        }
    },
    components:{
        Child
    },
    methods:{
        dataFn(data){
            this.message = data;
        }
    }
}
</script>
```

### 透传attribute (了解)
**概念**：传递给一个组件，却没有被该组件声明为props或emits的attribute或者v-on事件监听器。常见例子是class、style和id。当一个组件以单个元素为根作渲染时，透传的attribute会自动被添加到根元素上
```html
<template>
    <h3>Parent</h3>
    <Child class="attr-container"/>
</template>

<script>
import Child from "./Child.vue"
export default{
    components:{
        Child
    }
}
</script>
```
```html
<template>
    <!-- 必须是唯一根元素，若再下面在添加一个h4标签，则都不会生效红色 -->
    <h3>Child</h3>
</template>

<script>
export default{
    // 若想要禁用attribute继承则将下一行代码开放
    // inheritAttrs:false
}
</script>

<style>
.attr-container{
    color:red;
}
</style>
```

## 插槽slots
**概念**：帮助子组件接收模板内容。slot元素是一个插槽出口，表示了父元素提供的插槽内容将在哪里被渲染
```html
<template>
    <h3>Parent</h3>
    <!-- 这里得是双标签，而不是单标签 -->
    <Child>
        <div>
            <p>{{ message }}</p>
        </div>
    </Child>
</template>

<script>
import Child from "./Child.vue"
export default{
    data(){
        return{
            message:"插槽内容"
        }
    },
    components:{
        Child
    }
}
</script>
```
```html
<template>
    <h3>Child</h3>
    <slot></slot>
</template>
```

**插槽默认值**：在父级没有提供任何内容情况下，可以在子组件中指定默认内容
```html
<template>
    <h3>Child</h3>
    <slot>插槽默认值</slot>
</template>
```

**具名插槽**：在父组件中添加 `<template v-slot:header>` 或简写成 `<template #header>`
```html
<template>
    <h3>Parent</h3>
    <Child>
        <template #header>
            <p>{{ message }}</p>
        </template>
        <template #main>
            <p>内容</p>
        </template>
    </Child>
</template>

<script>
import Child from "./Child.vue"
export default{
    data(){
        return{
            message:"插槽内容"
        }
    },
    components:{
        Child
    }
}
</script>
```
```html
<template>
    <h3>Child</h3>
    <slot name="header">插槽默认值</slot>
    <slot name="main">插槽默认值</slot>
</template>
```

**插槽内容同时使用父和子组件域内的数据**：将子组件组件先传递给父组件，父组件将子组件数据和父组件数据一起传递给子组件。若是具名插槽，父组件中改成 `<template #header="slotProps">`，子组件中改成 `<slot name="header" :msg="childMessage">`
```html
<template>
    <h3>Parent</h3>
    <Child v-slot="slotProps">
        <p>{{ message }}-{{ slotProps.msg }}</p>
    </Child>
</template>

<script>
import Child from "./Child.vue"
export default{
    data(){
        return{
            message:"父组件数据"
        }
    },
    components:{
        Child
    }
}
</script>
```
```html
<template>
    <h3>Child</h3>
    <slot :msg="childMessage"></slot>
</template>

<script>
export default{
    data(){
        return{
            childMessage:"子组件数据"
        }
    }
}
</script>
```

## 组件生命周期
**生命周期函数**：
1. 创建期：`beforeCreate`、`created`
2. 挂载期：`beforeMount`、`mounted`
3. 更新期：`beforeUpdate`、`updated`
4. 销毁期：`beforeUnmount`、`unmounted`

**注意**：常用`mounted`发送请求、启动定时器、绑定自定义事件等；`beforeUnmount`清除定时器、解绑自定义事件等

<img src="https://i-blog.csdnimg.cn/direct/72eced7bffec4c738025384b31ccd2db.png#pic_center" width="600">

**应用**：
- 通过ref获取元素DOM结构
    ```html
    <template>
        <p ref="name">hi</p>
    </template>

    <script>
    export default{
        beforeMount(){
            console.log(this.$ref.name); // undefined
        },
        mounted(){
            console.log(this.$ref.name); // <p>hi</p>
        }
    }
    </script>
    ```
- 模拟网络请求渲染数据：页面都是先渲染结构再获取数据
    ```html
    <template>
        <ul>
            <li v-for="(item,index) of banner" :key="index">
                <h3>{{ item.title }}</h3>
                <p>{{ item.content }}</p>
            </li>
        </ul>
    </template>

    <script>
    export default{
        data(){
            return{
                banner:[]
            }
        },
        mounted(){
            <!-- 模拟网络请求 -->
            this.banner = [
                {
                    "title":"xxx",
                    "content":"xxx"
                },...
            ]
        }
    }
    </script>
    ```

## 动态组件
**作用**：方便两个组件间来回切换，比如Tab界面
```html
<template>
    <component :is="tabComponent"></component>
    <button @click="changeHandle">切换组件</button>
</template>

<script>
import ComponentA from "./component/ComponentA.vue"
import ComponentB from "./component/ComponentB.vue"
export default{
    data(){
        return{
            tabComponent:"ComponentA"
        }
    },
    components:{
        ComponentA,
        ComponentB
    },
    methods:{
        changeHandle(){
            this.tabComponent = this.tabComponent == "ComponentA" ? "ComponentB" : "ComponentA"
        }
    }
}
</script>
```

**组件保持存活**：当使用 `<component :is="">` 让多个组件间切换时，被切换掉的组件会被卸载，可通过 `<keep-alive>` 组件强制让被切换掉的组件保持存活状态
```html
<template>
    <keep-alive>
        <component :is="tabComponent"></component>
    </keep-alive>
    <button @click="changeHandle">切换组件</button>
</template>
```

## 异步组件：优化组件性能
**方法**：defineAsyncComponent
```html
<template>
    <component :is="tabComponent"></component>
    <button @click="changeHandle">切换组件</button>
</template>

<script>
import {defineAsyncComponent} from 'vue'
import ComponentA from "./component/ComponentA.vue"
// import ComponentB from "./component/ComponentB.vue"
// 异步加载组件。原来是第一次加载页面时两个组件都加载了，现在异步加载组件，第一次加载页面只有组件A被加载，只有当点击按钮后组件B才被加载
const ComponentB = defineAsyncComponent(() => 
    import("./component/ComponentB.vue")
)
export default{
    data(){
        return{
            tabComponent:"ComponentA"
        }
    },
    components:{
        ComponentA,
        ComponentB
    },
    methods:{
        changeHandle(){
            this.tabComponent = this.tabComponent == "ComponentA" ? "ComponentB" : "ComponentA"
        }
    }
}
</script>
```

## 依赖注入：跨组件透传
**问题**：当祖先组件的部分数据需要传递给一个较远的后代组件时，使用props须沿着组件链逐级传递下去，称为“prop逐级透传”<br>
**方法**：`provide` 和 `inject`，只能祖先向下传，不能反过来。一个父组件相对于其所有的后代组件，会作为依赖提供者，任何后代的组件树，无论层级有多深，都可以注入由父组件提供给整条链路的依赖

<img src="https://i-blog.csdnimg.cn/direct/aee15865d92b46f994a6755c8bac062d.png#pic_center" width="600">

祖宗-父亲-儿子的层级:
```html
<template>
    <h3>祖先</h3>
    <Parent/>
</template>

<script>
import Parent from "./Parent.vue"
export default{
    data(){
        return{
            message:"祖先的数据"
        }
    },
    // provide:{
    //     massage:"祖先的数据"
    // },
    // 若数据来源于data则使用以下代码，否则使用以上注释的代码
    provide(){
        return{
            massage: this.message
        }
    },
    components:{
        Parent
    }
}
</script>
```
```html
<template>
    <h3>Child</h3>
    <p>{{ message }}</p>
    <p>{{ fullMessage }}</p>
</template>

<script>
export default{
    inject:["message"],
    data(){
        return{
            fullMessage:this.message
        }
    }
}
</script>
```

除了在一个组件中提供依赖，还能在整个应用层面提供依赖
```js
import { createApp } from 'vue'
import App from './App.vue'
const app = createApp(App)
// 在main.js中写入provide全局数据，再其他组件内可用inject来使用这条全局数据
app.provide("globalData","全局数据")
app.mount('#app')
```

## Vuex
**概念**：Vue 的官方状态管理库，用于集中管理组件间共享的数据<br>
**工作原理**：

<img src="https://i-blog.csdnimg.cn/direct/f3026f2640934aeda220bde6c6175449.png#pic_center" width="500">

**使用**：
1. `npm i vuex`
2. 创建 Vuex Store：在 src/store/index.js 中定义 Store
    ```js
    import { createStore } from 'vuex'

    export default createStore({
        state: {
            count: 0,
            user: null
        },
        // 简单状态变更（如计数器增减、切换布尔值）直接使用Mutation
        mutations: {
            increment(state, amount) {
                state.count += amount
            },
            setUser(state, user) {
                state.user = user
            }
        },
        // 异步操作（如 API 请求、定时器）先 Action 再 Mutation
        actions: {
            async fetchUser({ commit }, userId) {
                const user = await api.getUser(userId) // 模拟 API 请求
                commit('setUser', user)
            }
        },
        // getters不是必须使用的，能将state中的数据进行加工
        getters: {
            doubleCount: (state) => state.count * 2
        }
    })
    ```
3. 将 Store 注入 Vue 应用：main.js中加入
    ```js
    import { createApp } from 'vue'
    import App from './App.vue'
    import store from './store' // 导入 Store

    const app = createApp(App)
    app.use(store) // 注入 Store
    app.mount('#app')
    ```
4. 在组件中使用
    ```js
    <template>
    <div>
        <p>Count: {{ count }}</p>
        <p>Double: {{ doubleCount }}</p>
        <button @click="increment(3)">+3</button>
    </div>
    </template>

    <script>
    import { mapState, mapGetters, mapMutations, mapActions } from 'vuex'
    export default {
        computed: {
            // 使用 mapState 映射 state.count
            ...mapState(['count']),
            // 使用 mapGetters 映射 getters.doubleCount
            ...mapGetters(['doubleCount'])
        },
        methods: {
            // 使用 mapMutations 映射 mutations.increment
            ...mapMutations(['increment']),
            // 使用 mapActions 映射 actions.fetchUser
            ...mapActions(['fetchUser'])
        }
    };
    </script>
    ```
**拆分为模块**：
1. 目录结构
    ```
    src/
    store/
        index.js       # 主入口文件
        modules/
        counter.js   # 计数器模块
        api.js       # API 请求模块
    ```
2. 模块定义
- 计数器模块 (store/modules/counter.js)
    ```js
    const counter = {
    namespaced: true, // 启用命名空间
    state: {
        count: 0
    },
    mutations: {
        increment(state, amount) {
        state.count += amount;
        }
    },
    actions: {
        incrementAsync({ commit }, payload) {
        setTimeout(() => {
            commit('increment', payload.amount);
        }, 1000);
        }
    },
    getters: {
        doubleCount: (state) => state.count * 2
    }
    };

    export default counter
    ```
- API 请求模块 (store/modules/api.js)
    ```js
    const api = {
    namespaced: true, // 启用命名空间
    state: {
        user: null
    },
    mutations: {
        setUser(state, user) {
        state.user = user;
        }
    },
    actions: {
        async fetchUser({ commit }, userId) {
        const user = await mockApi.getUser(userId); // 模拟 API 请求
        commit('setUser', user);
        }
    }
    };

    // 模拟 API
    const mockApi = {
    getUser: (userId) => {
        return new Promise((resolve) => {
        setTimeout(() => {
            resolve({ id: userId, name: 'User ' + userId });
        }, 500);
        });
    }
    };

    export default api
    ```
3. 主 Store 文件 (store/index.js)
    ```js
    import { createStore } from 'vuex';
    import counter from './modules/counter';
    import api from './modules/api';

    export default createStore({
    modules: {
        counter,
        api
    }
    })
    ```
4. 组件中使用（带命名空间）
    ```js
    <template>
    <div>
        <!-- 计数器模块 -->
        <p>Count: {{ count }}</p>
        <p>Double: {{ doubleCount }}</p>
        <button @click="increment(1)">+1</button>
        <button @click="incrementAsync({ amount: 2 })">+2 Async</button>

        <!-- API 模块 -->
        <p>User: {{ user?.name }}</p>
        <button @click="fetchUser(123)">Fetch User</button>
    </div>
    </template>

    <script>
    import { mapState, mapGetters, mapMutations, mapActions } from 'vuex';

    export default {
    computed: {
        // 计数器模块
        ...mapState('counter', ['count']),
        ...mapGetters('counter', ['doubleCount']),
        // API 模块
        ...mapState('api', ['user'])
    },
    methods: {
        // 计数器模块
        ...mapMutations('counter', ['increment']),
        ...mapActions('counter', ['incrementAsync']),
        // API 模块
        ...mapActions('api', ['fetchUser'])
    }
    };
    </script>
    ```

## Pinia
**与Vuex对比**：去掉了mutation，提供符合组合式风格的API，去掉了modules的概念，每一个store都是一个独立的模块，搭配TypeScript一起使用提供可靠的类型推断
**使用**：
1. `npm install pinia`
2. 在main.js文件中
    ```js
    import{createPinia} from 'pinia'
    const pinia = createPinia()
    createApp(App).use(pinia).mount('#app')
    ```
3. 创建store
    ```js
    // stores/counter.js
    import { defineStore } from 'pinia'
    import { ref, computed } from 'vue'

    export const useCounterStore = defineStore('counter', () => {
        // 数据(state)
        const count = ref(0)
        // action 同步+异步
        function increment() {
        count.value++
        }
        // getter
        const doubleCount = computed(() => count.value * 2)

        return { count,increment,doubleCount }
    })
    ```
    异步action：
    ```js
    const API_URL = 'http://...'
    const list = ref([])
    const loadList = async () => {
        const res = await axios.get(API_URL)
        list.value = res.data.data.channels
    }
    ```
4. 在组件中使用
    ```js
    <script setup>
    import { useCounterStore } from './stores/counter'
    const { countStore } = useCounterStore()
    </script>

    <template>
    <div>
        <h2>Count: {{ countStore.count }}</h2>
        <button @click="countStore.increment">+1</button>
        <h2>{{ countStore.doubleCount }}</h2>
    </div>
    </template>
    ```
### storeToRefs
**解决**：可以辅助保持数据(state+getter)的响应式解构
```js
import { storeToRefs } from 'pinia'
const { count, doubleCount } = storeToRefs(counterStore)
```
*注意：store中的方法还是需要直接解构的
```js
const { increment } = counterStore
```

## vue-router
**路由概念**：路由route就是一组key-value的对应关系，key为路径，value可能是function或component。多个路由，需要经过路由器router的管理<br>
**路由分类**：
1. 前端路由：
    - value是component，用于展示页面内容
    - 工作过程：当浏览器的路径改变时，对应组件就会显示
2. 后端路由
    - value是function，用于处理客户端提交的请求
    - 工作过程：服务器接收到一个请求时，根据请求路径找到匹配的函数来处理请求，返回响应数据

**概念**：vue中的一个插件库，用来实现SPA (single page web application) 应用<br>
**SPA应用概念**：
1. 单页Web应用
2. 整个应用只有一个完整的页面
3. 点击导航链接不会刷新页面，只会做页面的局部更新
4. 数据需要通过ajax请求获取

<img src="https://i-blog.csdnimg.cn/direct/752ddfb73f0f4b15820a74017cfddec5.png#pic_center" width="600">

**使用**：
1. `npm i vue-router`
2. 在项目中新建文件夹router，内新建index.js (可以将路由组件放置在pages文件夹下，一般组件放在components文件夹下)
    ```js
    import { createRouter, createWebHistory } from 'vue-router'

    const router = createRouter({
        history: createWebHistory(), // 去除URL中的 #符号
        routes: [
            { path: '/counttool', component: () => import('../pages/CountTool.vue') }, 
        ],
    })

    export default router
    ```
3. 在项目的main.js中引入
    ```js
    import { createApp } from 'vue'
    import App from './App.vue'
    import router from './router'

    const app = createApp(App)
    app.use(router)
    app.mount('#app')
    ```
4. 实现切换 (RouterLink会转成a标签，active-class可配置点击实现高亮样式) 
`<RouterLink active-class="active" to="/counttool">CountTool</RouterLink>`
5. 指定展示位置
`<RouterView></RouterView>`

*注意：当路由切换时，离开的页面组件会被销毁，新进入的页面组件会重新创建

**嵌套(多级)路由使用**：
1. 修改router/index.js中代码
    ```js
    const router = createRouter({
        history: createWebHistory(),
        routes: [
            { 
                path: '/counttool', 
                component: () => import('../pages/CountTool.vue'),
                children: [
                    {
                        path: 'news',  // 这里不需要加 '/'
                        component: () => import('../pages/News.vue')
                    }
                ]
            },
        ],
    })
    ```
2. 访问方式 (要写完整路径)
`<RouterLink to="/counttool/news">新闻</RouterLink>`

**query参数**：
1. 传递参数：：注意携带query参数既能使用命名路由，又能使用path
    ```js
    <ul>
        <li v-for="m in messageList" :key="m.id">
            <RouterLink :to="{
                path:'/counttool/news'
                query:{
                    id:m.id,
                    title:m.title
                }
            }">
                {{m.title}}
            </RouterLink>
        </li>
    </ul>
    ```
2. 接收参数
    ```
    $route.query.id
    $route.query.title
    ```

**params参数**：
1. 路由配置router/index.js
    ```js
    {
        // 命名路由
        name: 'article',
        path: '/article/:category/:title',
        component: () => import('../pages/Article.vue')
    }
    ```
2. 传递参数：注意携带params参数的对象写法只能使用命名路由
    ```js
    <ul>
        <li v-for="m in messageList" :key="m.id">
            <RouterLink :to="{
                name:'article'
                params:{
                    id:m.id,
                    title:m.title
                }
            }">
                {{m.title}}
            </RouterLink>
        </li>
    </ul>
    ```
3. 接收参数
    ```
    $route.params.id
    $route.params.title
    ```

**路由的props配置**：让路由组件更方便的收到参数
1. 路由配置router/index.js
    ```js
    {
        name: 'article',
        path: '/article/:category/:title',
        component: () => import('../pages/Article.vue')
        // 第一种写法，值为对象，会以props的形式传递给组件
        props:{a:1}
        // 第二种写法，值为布尔值，会把该组件收到的所有params参数以props的形式传递给组件
        props:true
        // 第三种写法，值为函数
        props($route){
            return {id:$route.query.id, tltie:$route.query.title}
        }
    }
    ```
2. 在Article.vue中
    ```
    props:['id', 'title']
    ```

**编程式路由导航**：不借助RouterLink实现路由跳转
- `$router.forward()`：前进
- `$router.back()`：后退
- `$router.go(number)`：number正数前进number步，负数反之
- `$router.push(...)`：跳转新页面，新增历史记录
    ```js
    <template>
        <ul>
            <li v-for="m in messageList" :key="m.id">
                <button @click="pushShow(m)">push方式</button>
            </li>
        </ul>
    </template>
    
    <script>
        export default {
            data(){
                return{
                    messageList:[...]
                }
            },
            methods:{
                pushShow(m){
                    this.$router.push({
                        name:'article'
                        query:{
                            id:m.id,
                            title:m.title
                        }
                    })
                }
            }
        }
    </script>
    ```
- `$router.replace(...)`：跳转新页面，替换当前历史记录

### 路由元meta
**概念**：是vue-router中路由配置的一部分，用于存放自定义的元信息
```js
{
  path: '/dashboard',
  component: Dashboard,
  meta: {
    // 标记这个页面是否需要登录权限
    requiresAuth: true,
    title: '仪表盘'
  }
}
```

### 路由守卫
**概念**：用于在路由跳转前或跳转后，执行特定逻辑，比如权限验证、登录检查、数据加载等<br>
**守卫类型**：
1. beforeEach 全局前置守卫 —— 初始化的时候被调用、每次路由切换之前被调用
    ```js
    // router/index.js 
    router.beforeEach((to, from, next) => {
        if (to.meta.requiresAuth) {
            if(localStorage.getItem('student') === 'wjn'){
                next()
            } else {
                alert('无权限查看')
            }
        } else {
            next()
        }
    })
    ```
2. afterEach 全局后置守卫 —— 初始化的时候被调用、每次路由切换之后被调用
    ```js
    router.afterEach((to, from) => {
        if (to.meta.title) {
            document.title = to.meta.title
        }
    })
    ```
3. beforeEnter 路由独享守卫 —— 定义在单个路由配置中，只对该路由生效
    ```js
    {
        path: '/admin',
        component: () => import('./views/Admin.vue'),
        beforeEnter: (to, from, next) => {
            const isAdmin = localStorage.getItem('role') === 'admin'
            if (isAdmin) {
                next()
            } else {
                next('/no-permission')
            }
        }
    }
    ```
4. 组件内守卫
    - beforeRouteEnter —— 通过路由规则，进入该组件时被调用
    - beforeRouteLeave —— 通过路由规则，离开该组件时被调用

### 路由模式
1. Hash 模式（默认） —— url中带 #，# 后面的路径不会被发送到服务器
    ```js
    const router = createRouter({
        history: createWebHashHistory(),
        ...
    })
    ```

2. History 模式 —— 刷新页面或直接访问某个路径时会向服务器请求对应路径的文件；应用部署上线时需要后端人员支持，解决刷新页面服务器404的问题
    ```js
    const router = createRouter({
        history: createWebHistory(),
        ...
    })
    ```

## Vue2和Vue3实现响应式对比
**Vue2**:
- 对象类型：通过Object.defineProperty()对数据的读取、修改进行拦截(数据劫持)
- 数组类型：通过重写更新数组的一系列方法来实现拦截。(对数组的变更方法进行了包裹)
```js
Object.defineProperty(data,'count',{
    get(){},
    set(){}
})
```
*存在问题：新增和删除属性，界面不会更新。无法通过下标修改数组。(但这些问题都可以通过其他方法解决)

**Vue3**:
- 通过Proxy(代理)：拦截对象中任意属性的变化，包括属性值的读写、属性的添加、属性的删除等
- 通过Reflect(反射)：对源对象的属性进行操作
```js
new Proxy(target, {
    get(target, prop) {
      return Reflect.get(target, prop)
    },
    set(target, prop, value) {
      return Reflect.set(target, prop, value)
    },
    deleteProperty(target, prop) {
      return Reflect.deleteProperty(target, key)
    }
})
```

# Vue3
## 组合式API入口 — setup
**触发时机**：在生命周期beforeCreate之前<br>
**this指向**：指向undefined<br>

## ref和reactive
**作用**：用函数调用的方式生成响应式数据<br>
**对比**：
1. reactive不能处理简单类型数据
2. ref参数类型支持更好但是必须通过.value属性访问修改
3. ref函数的内部实现依赖于reactive函数

**使用**：
```js
<script setup>
import { ref, reactive } from 'vue'

// 基本类型用 ref
const count = ref(0)
const increment = () => {
    count.value++
}

// 对象用 reactive
const user = reactive({
    name: 'wu',
    age: 18
})
const add = () => {
    user.age++
}
</script>
```

## computed
```js
<script setup>
import { computed } from 'vue'

const computedState = computed(() => {
    return 计算后的值
})
</script>
```

## watch
```js
<script setup>
import { ref, watch } from 'vue'
const count = ref(0)
const name = ref('wu')

watch(count, (newValue, oldValue) => {
    console.log(newValue)
})
// 侦听多个数据源
watch([count, name], ([newCount, newName], [oldCount, oldName]) => {
    console.log('count或name发生改变')
})
// 侦听器创建时立即触发回调immediate
watch(count, () => {
    console.log('count发生改变')
},{
    immediate: true
})
// ref对象默认浅层侦听，直接修改嵌套的对象属性不会触发回调执行，需开启deep
const state = ref({count:0})
watch(state, () => {
    console.log('count发生改变')
},{
    deep: true
})
// 精确侦听对象的某个属性
const info = ref({
    name:'wu',
    age:18
})
watch(
    () => info.value.age,
    () => console.log('age改变了')
)
</script>
```

## watchEffect
**概念**：自动收集依赖、立即执行、无新旧值、不适合部分依赖监听
```js
import { ref, watchEffect } from 'vue'
const count = ref(0)

watchEffect(() => {
  console.log(`自动监听count，现在是 ${count.value}`);
})
```

## 生命周期

<img src="https://i-blog.csdnimg.cn/direct/aec2fa76603e444aa54c02cfa83edec3.png#pic_center" width="600">

```js
<script setup>
import { onMounted } from 'vue'

onMounted(() => {
    ...
})
</script>
```
*注意：生命周期函数可以执行多次，多次执行时传入的回调会在时机成熟时依次执行

## 父传子
```js
<script setup>
// 引入后无需注册就能使用
import Son from './son.vue'
</script>

<template>
    <Son message="father message"/>
</template>
```
```js
<script setup>
// 通过defineProps "编译器宏" 接收传递的数据
const props = defineProps({
    message:String
})
</script>

<template>
    {{message}}
</template>
```

## 子传父
```js
<script setup>
import Son from './son.vue'
const getMessage = (msg) => {
    console.log(msg)
}
</script>

<template>
    <Son @get-message="getMessage" />
</template>
```
```js
<script setup>
// 通过defineEmits编译器宏生成emit方法
const emit = defineEmits(['get-message'])
const sendMsg = () => {
    emit('get-message', 'son message')
}
</script>

<template>
    <button @click="sendMsg">发送数据</button>
</template>
```

## 模板引用
### 获取dom
```js
<script setup>
import { ref } from 'vue'
// 获取的dom存放在h1Ref.value中
const h1Ref = ref(null)
</script>

<template>
    <h1 ref="h1Ref">h1标签</h1>
</template>
```

### defineExpose()
**作用**：默认情况下组件内部的属性和方法是不开放给父组件访问的，通过defineExpose编译宏指定哪些属性和方法可以允许访问

## 跨层组件通信
### 顶层传底层
1. 顶层组件通过`provide`函数提供数据
    ```js
    provide('key', 顶层数据)
    ```
2. 底层组件通过`inject`函数获取数据
    ```js
    const message = inject('key')
    ```

顶层传底层方法，实现底层修改顶层的数据：
```js
// 顶层组件中
const count = ref(0)
const setCount = () => {
    count.value++
}
provide('setCount-key', setCount)
```
```js
// 底层组件中
<script setup>
import { inject } from 'vue'
const setCount = inject('setCount-key')
</script>

<template>
    <button @click="setCount">修改数据</button>
</template>
```