# 设计模式

## 工厂模式
**概念**：是创建对象对象的一种方式，不暴露创建对象的具体逻辑，将逻辑封装在一个函数内，这个函数可以被视为一个工厂<br>
**场景**：
1. jQuery的$函数
2. React createElement函数 (jsx语法的底层函数)

## 单例模式
**概念**：全局唯一实例<br>
**场景**：
1. Vue项目中的Vue实例
2. Node项目中的App实例
3. Vuex和Redux中的store

## 代理模式
**概念**：控制对象访问<br>
**场景**：
1. proxy构建函数

## 观察者模式
**概念**：定义了对象间的一种一对多的依赖关系，当一个对象的状态发生变化时，所有依赖于它的对象都得到通知，并自动更新 (没有媒介)<br>
**场景**：
1. addEventListener

## 发布订阅者模式
**概念**：发布者和订阅者互不认识，中间有第三方媒介<br>
**场景**：
```js
function fn1(){
    // 事件函数1
}
function fn2(){
    // 事件函数2
}

// 开启自定义事件监听，其中第三方是eventbus
eventBus.on("eventName", fn1); // 订阅者1
eventBus.on("eventName", fn2); // 订阅者2

// 触发自定义事件eventName，从而执行fn1函数
eventBus.$emit('eventName'); // 发布者$emit

// 删除自定义事件，防止内存泄漏，在生命周期中的销毁阶段
eventBus.off('eventName', fn1);
```

## 装饰器模式
**概念**：保证原有函数功能不变的同时，增加一个新的功能<br>
**场景**：
1. ES和TypeScript的Decorator语法
2. 装饰器类型：类装饰器，函数(方法)装饰器，属性装饰器……
```js
function deco(){
    return function(){
        console.log("新功能")
    }
}

@deco()
function fn(){
    console.log("原本功能")
}
```