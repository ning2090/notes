# ES6
**简介**：ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。它的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

## let和const
### let变量
**特性**：
1. 不存在变量提升，声明的变量一定在声明后使用，否则报错。这在语法上，称为*暂时性死区*(temporal dead zone，简称 TDZ)
    ```js
    // 传统var该写法不会报错，控制台会输出undefined
    console.log(a);
    var a = 3;
    ```
2. 块级作用域，如下图会报错
    ```js
    if(1===1){
        let a = 3;
    }
    console.log(a);
    ```
3. 在相同作用域内，不允许重复声明

### const常量
**特性**：
1. 声明只读的常量。一旦声明变量，就必须立即初始化，不能留到以后赋值，并且声明后不可修改
2. 不存在变量提升
3. 块级作用域
4. 在相同作用域内，不允许重复声明

## 模板字符串
**用法**：用反引号把结构包裹起来，变量处用`${变量名}`
```js
const oBox = document.querySelector('.box');
let id = 1, name = '小马哥';
//传统写法
let htmlTel = "<ul><li><p>id:" + id + "</p><p>name:" + name + "</p></li></ul>";
//ES6写法
let htmlTel = `<ul>
    <li>
        <p>id:${id}</p>
        <p>name:${name}</p>
    </li>
</ul>`;
oBox.innerHTML = htmlTel;
```

## 函数默认值
1. 带参数默认值的函数
    ```js
    // b=0表示当未传递b参数时，b默认值为0
    function add(a, b = 0){
        return a + b;
    }
    add(10); // 结果为10
    ```
2. 默认的表达式也可以是一个函数
    ```js
    function getVal(val) {
    return val + 5;
    }
    function add(a, b = getVal(5)) {
    return a + b;
    }
    console.log(add(10)); // 结果20
    ```

## 剩余参数
**用法**：剩余运算符用于将一个不定数量的参数表示为一个数组，由三个点...和一个紧跟着的具名参数指定
```js
function checkArgs(...args){
  // ...args解决了arguments的问题
  console.log(args);
}

checkArgs('a','b','c')//结果["a", "b", "c"]
```

## 扩展运算符
**用法**：用于将一个数组或类数组对象展开为一系列元素，由三个点...和一个紧跟着的具名参数指定
```js
const arr = [10, 20, 50, 30, 90, 100, 40];
console.log(Math.max(...arr));//结果100
```

## 箭头函数
**用法**：`()=>{}` 等价于 `function(){}`
```js
// 有一个参数
let fn1 = value => value;
// 有两个参数
let add = (value,value2) => value + value2;
// 无参数
let fn = () => "hello world";
// 如果箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错
let getId = id => ({id: id, name: 'wu'})
```
**注意点**：
1. 没有this绑定。箭头函数内部的this值只能通过查找作用域链来确定。一旦使用箭头函数，当前就不存在作用域链。如果箭头函数被一个非箭头函数所包括，那么this的值与该函数的所属对象相等，否则 则是全局的window对象
    ```js
    let PageHandler = {
    id: 123,
    init: function () {
        document.addEventListener('click', (event) => {
            console.log(this);
            this.doSomeThings(event.type);
        }, false);
    },
    doSomeThings: function (type) {
        console.log(`事件类型:${type},当前id:${this.id}`);
    }
    }
    PageHandler.init();
    ```
2. 箭头函数中没有arguments对象
    ```js
    var getVal = (a,b) => {
        console.log(arguments);
        return a + b;
    }
    console.log(getVal(1,2)); //arguments is not defined
    ```
3. 箭头函数不能使用new关键字来实例化对象
    ```js
    let Person = ()=>{}
    let p1 = new Person();// Person is not a constructor
    ```

## 解构赋值
**概念**：解构赋值是对赋值运算符的一种扩展。它通常针对数组和对象进行操作
### 数组解构
**用法**：`let [a,b,c] = [1,2,3];` 如果解构不成功，变量的值就等于undefined
### 对象解构
**用法**：
```js
let obj = {
    a:{
        name:'张三'
    },
    b:[],
    c:'hello world'
}
// 不完全解构，可忽略b,c属性
let {a} = obj;
// 剩余运算符 使用此法将其它属性展开到一个对象中存储
let {a,...res} = obj;
console.log(a,res);
```

## 数组的扩展方法
1. from() 将伪数组转换成真正的数组
    ```js
    function add(){
    let arr = Array.from(arguments);
    console.log(arr);
    }
    add(1,2,3);// (3) [1, 2, 3]

    // from() 还可以接受第二个参数，用来对每个元素进行处理
    let lis = document.querySelectorAll('li')
    let liContents = Array.from(lis, ele => ele.textContent);
    ```
2. of() 将任意的数据类型，转换成数组
    ```js
    console.log(Array.of(3,[1,2,3],{id:1})); // (3) [3, Array(3), {...}]
    ```
3. copywithin() 数组内部将指定位置的元素复制到其他的位置，返回当前数组
    ```js
    // 表示从3位置往后的所有数值，替换从0位置往后的三个数值
    console.log([1,2,3,8,9,10].copyWithin(0,3)); // [8,9,10,8,9,10]
    ```
4. find() 找出第一个符合条件的数组成员，findIndex() 找出第一个符合条件的数组成员的索引
    ```js
    let num = [1, 2, -10 , -20, 9, 2].find(n => n < 0)
    console.log(num);// -10

    let numIndex = [1, 2, -10 , -20, 9, 2].findIndex(n => n < 0)
    console.log(numIndex);// 2
    ```
5. keys() values() entries() 都返回一个遍历器*Iterator*，可以使用for...of循环进行遍历，其中keys()对键名遍历，values()对值遍历，entries()对键值对遍历
    ```js
    for(let index of ['a', 'b'].keys()){
        console.log(index);// 会输出0和1
    }

    for(let ele of ['a', 'b'].values()){
        console.log(ele);// 会输出a和b
    }

    for(let [index,ele] of ['a', 'b'].entries()){
        console.log(index,ele);
    }
    ```
6. includes() 返回一个布尔值，表示某个数组是否包含给定的值，替换了之前的indexOf()
    ```js
    console.log([1,2,3].includes(2));// true
    ```

## 对象的扩展
### 属性的简洁表示法
例子1：
```js
const name = '张三';
const age = 19;
const person = {
    name, //等同于name:name
    age,
    // 方法也可以简写
    sayName() {
        console.log(this.name);
    }
}
person.sayName();
```
例子2：用于函数的返回值
```js
function fn(x, y) {
  return {x, y};
}
console.log(fn(10, 20));
```
### 属性名的表达式
**用法**：
```js
const name = 'a';
const obj = {
  isShow:true,
  [name + 'bc']:123,
  ['f' + name](){
    console.log(this);
  }
}
console.log(obj);// {isShow: true, abc: 123, fbc: f}
```
### 对象的方法
1. `is()` 替换了原来的 `===`
    ```js
    console.log(NaN === NaN);// false
    console.log(Object.is(NaN,NaN));// true
    ```
2. `Object.assign(target, obj1, obj2, ...)` 对象的合并，返回合并之后的新对象
    ```js
    let newObj = Object.assign({}, {a:1}, {b:2});
    console.log(newObj);// {a: 1, b: 2}
    ```
## Symbol类型
**概念**：原始数据类型Symbol，表示是独一无二的值，用来定义对象的私有变量
**用法**：
```js
const name = Symbol('name');
const name2 = Symbol('name');
console.log(name === name2);// false
console.log(name);// Symbol(name)

let obj = {
  [name]: 'wu'
};
// 若用Symbol定义的对象中的变量，取值时一定要用[变量名]
console.log(obj[name]);// wu

// 获取Symbol声明的属性名(作为对象的key)
// 方法一
let s = Object.getOwnPropertySymbols(obj);
console.log(s[0]);// Symbol(name)
// 方法二
let m = Reflect.ownKeys(obj);
console.log(m[0]);// Symbol(name)
```
*注意点：对象中定义的是Symbol的话就没有遍历

## Set集合数据类型
**概念**：表示无重复值得有序列表<br>
**用法**：
```js
let set = new Set();
console.log(set);// Set(0) {}

// 添加元素
set.add(2);
set.add('3');
set.add('3');
set.add([1,2,3]);

// 删除元素
set.delete(2);
console.log(set);// Set(2) {"3", Array(3)}

// 校验某个值是否在set中
console.log(set.has('3'));// true

// 访问集合长度
console.log(set.size);// 2

// 将set转换成数组
let set2 = new Set([1,2,3,3,3]);
let arr = [...set2]
console.log(arr);// (4) [1, 2, 3]
```
*注意：set中添加了一个对象，用obj = null来释放当前的资源，但是set中对象的引用无法被释放，解决办法可以使用WeakSet，但是WeakSet不能传入非对象类型的参数，不可迭代，没有forEach()，没有size属性

## Map数据类型
**概念**：Map类型是键值对的有序列表，键和值都是任意类型<br>
**用法**：
```js
let map = new Map();

// 设置值
map.set('name','wu');
console.log(map);// Map(1) {"name" => "wu"}

// 获取值
console.log(map.get('name'));// wu

// 校验某个值是否在map中
map.has('name');

// 删除值
map.delete('name');

// 清除map
map.clear();

let m = new Map([
  ['a', 1],
  ['b', 2]
]);
console.log(m);// Map(2) {"a" => 1, "b" => 2}
```

## 迭代器Interator
**概念**：是一种新的遍历机制。第一个核心，迭代器是一个接口，能快捷的访问数据；第二个核心，迭代器是用于遍历数据结构的指针，类似于数据库的游标<br>
**用法**：
```js
const items = ['one', 'two'];
// 1. 通过Symbol.iterator来创建迭代器
const ite = items[Symbol.iterator]();
// 2. 通过迭代器的next()来获取迭代之后的结果，其中done为false表示遍历继续，否则为遍历完成
console.log(ite.next()); // {value: "one", done: false}
console.log(ite.next()); // {value: "two", done: false}
console.log(ite.next()); // {value: undefined, done: true}
```

## 生成器Generator
**概念**：通过yield关键字，将函数挂起，为改变执行流提供了可能，同时为做异步编程提供了方案<br>
**与普通函数的区别**：其一是function后函数名前有个*，另外只能在函数内部使用yield表达式，让函数挂起<br>
**用法**：
```js
function* func(){
  console.log('one')
  yield 1;
  console.log('two')
  yield 2;
  console.log('end')
}
// 返回一个遍历器对象，可以调用next()
let fn = func();
// generator函数是分段执行的，yield语句是暂停执行，而next()恢复执行
console.log(fn.next());// 先输出one，后输出{value: 1, done: false}
console.log(fn.next());// 先输出two，后输出{value: 2, done: false}
console.log(fn.next());// 先输出end，后输出{value: undefined, done: true}

function* add(){
  console.log('start');
  // 这里的x不是yield '2'的返回值，它是next()调用，恢复当前yield()执行传入的实参
  let x = yield '2';
  console.log('one:' + x);
  let y = yield '3';
  console.log('two:' + y);
  return x + y;
}
const fn = add();
console.log(fn.next());// 先输出start，后输出{value: "2", done: false}
console.log(fn.next(20));// 先输出one:20，后输出{value: "3", done: false}
console.log(fn.next(30));// 先输出two:30，后输出{value: 50, done: true}
```
**使用场景1**：为不具备Interator接口的对象提供了遍历操作
```js
function* objectEntries(obj){
  //获取对象的所有的key保存到数组[name, age]
  const propKeys = Object.keys(obj);
  for(const propkey of propKeys){
    yield [propkey, obj[propkey]]
  }
}

const obj = {
  name:'wu',
  age:18
}
obj[Symbol.iterator] = objectEntries;

for(let [key,value] of objectEntries(obj)){
  console.log(`${key}:${value}`);//先输出name:wu，后输出age:18
}
```
**使用场景2**：部署ajax操作，让异步代码同步化。例如调用一个接口，请求成功中接着调用一个接口，这样反复，解决这种叫做“回调地狱”的问题
```js
function* main(){
  let res = yield request('https://...')
  console.log(res);
}
const ite = main();
ite.next();
function request(url){
  $.ajax({
    url,
    method:'get',
    success(res){
      ite.next(res);
    }
  })
}
```
## Promise对象
**概念**：Promise代表了一个异步操作的最终完成（或失败）及其结果值。它允许你为异步操作的成功和失败分别指定回调函数，并且可以在这些回调函数之间进行链式调用，从而避免了传统的“回调地狱”（Callback Hell）问题。
**特点**：
1. 对象的状态不受外界影响，处理异步操作三个状态：pending(等待态)，fulfilled(成功态)，rejected(失败态)
2. 状态只能由 Pending 变为 Fulfilled 或由 Pending 变为 Rejected ，且状态改变之后不会在发生变化，会一直保持这个状态
### resolve 和 reject
- resolve : 将Promise对象的状态从 Pending(等待中) 变为 Fulfilled(已成功)
- reject : 将Promise对象的状态从 Pending(等待中) 变为 Rejected(已失败)
```js
let promise = new Promise((resolve, reject) => {  
  setTimeout(() => {  
    resolve('成功的结果');  

    reject('失败的原因');  
  }, 1000);  
});  
  
// 使用.then()的链式调用处理成功的情况，使用.catch()捕获所有错误  
// then()第一个参数是resolve回调函数，第二个参数是可选的，是reject状态回调
// then()返回一个新的promise示例，可以采用链式编程
promise.then(  
  (value) => {  
    console.log(value); // '成功的结果'
  }  
).then(  
  (newValue) => {  
    console.log(newValue);  
  }  
).catch(  
  (error) => {  
    console.error('出错了：', error);  
  }  
);
```
*注意：catch(err=>{})方法等价于then(null,err=>{})

### resolve()和reject()方法
**概念**：resolve()方法将现有对象转换成Promise对象，该实例的状态为fulfilled。reject()方法返回一个新的Promise实例，该实例的状态为rejected<br>
**用法**：`let p = Promise.resolve('foo');` 等价于 `let p = new Promise(resolve=>resolve('foo'));`。<br>`let p2 = Promise.reject(new Error('出错了'));` 等价于 `let p2 = new Promise((resolve,reject)=>reject(new Error('出错了)));`

### all()方法
**概念**：all()方法提供了并行执行异步操作的能力，并且再所有异步操作执行完后才执行回调<br>
**用法**：
```js
let promise1 = new Promise((resolve, reject) => {});
let promise2 = new Promise((resolve, reject) => {});
let promise3 = new Promise((resolve, reject) => {});

let p4 = Promise.all([promise1, promise2, promise3])

p4.then(()=>{
    // 三个都成功 才成功
}).catch(err=>{
    // 如果有一个失败 则失败
})
```

### race()方法
**概念**：race()方法给某个异步请求设置超时时间，并且在超时后执行相应的操作<br>
**用法**：
```js
function requestImg(imgSrc){
    return new Promise((resolve,reject)=>{
        const img = new Image();
        img.onload = function(){
            resolve(img);
        }
        img.src = imgSrc;
    })
}

function timeout(){
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            reject(new Error('图片请求超时'))
        },3000);
    })
}

Promise.race([requestImg('https://...'),timeout()]).then(data=>{
    console.log(data);
    document.body.appendChild(data);
}).catch(err=>{
    console.log(err);
})
```