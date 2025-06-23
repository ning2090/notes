# 创建uni-app
**vue3+js**：`npx degit dcloudio/uni-preset-vue#vite my-vue3-project`

# 组件
只列出常用组件及其属性，具体查看 <a href="https://uniapp.dcloud.net.cn/component/">https://uniapp.dcloud.net.cn/component/</a>
## view
|属性名|类型|默认值|说明|
|--|--|--|--|
|hover-class|String|none|按下去的样式类|
|hover-stop-propagation|Boolean|false|是否阻止本节点的祖先节点出现点击态，App、H5、支付宝小程序、百度小程序不支持|
|hover-start-time|Number|50|按住后多久出现点击态，单位毫秒|
|hover-stay-time|Number|400|手指松开后点击态保留时间，单位毫秒|

**hover-class示例**：
```js
<template>
    <view class="box" hover-class="boxHover">hi</view>
</template>

<style lang="scss">
.box {
    width: 200px;
    height: 200px;
    background: #ccc;
}
.boxHover {
    background: pink;
}
</style>
```

## text
**概念**：view标签包裹的文字不能选中，需使用text标签
|属性名|类型|默认值|说明|
|--|--|--|--|
|user-select|Boolean|false|文本是否可选|
|space|String||显示连续空格。ensp中文字符空格一半大小、emsp中文字符空格大小、nbsp根据字体设置的空格大小|

## image
**mode属性值**：
|属性值|说明|
|--|--|
|scaleToFill|不保持纵横比缩放图片，使图片的宽高完全拉伸至填满 image 元素|
|aspectFit|保持纵横比缩放图片，使图片的长边能完全显示出来。也就是说，可以完整地将图片显示出来|
|aspectFill|保持纵横比缩放图片，只保证图片的短边能完全显示出来。也就是说，图片通常只在水平或垂直方向是完整的，另一个方向将会发生截取|
|widthFix|宽度不变，高度自动变化，保持原图宽高比不变|
|heightFix|高度不变，宽度自动变化，保持原图宽高比不变|

## navigator
 **概念**：类似于a标签。也可通过API中的 `uni.navigateTo(OBJECT)` 实现跳转
|属性名|类型|默认值|说明|
|--|--|--|--|
|url|String||跳转链接，注意不能加.vue 后缀|
|open-type|String|navigate|跳转方式。navigate保留当前页面并跳转到应用内的某个页面 (有回退按键)、reLaunch关闭所有页面并打开到应用内的某个页面、redirect关闭当前页面并跳转到应用内的某个页面、navigateBack关闭当前页面并返回上一页面或多级页面|
|target|String|self|跳转到其他某个小程序，默认当前小程序|

## button
|属性名|类型|默认值|说明|
|--|--|--|--|
|size|String|default|按钮的大小。default默认大小、mini小尺寸|
|type|String|default|按钮的样式类型。primary、default白色、warn红色|
|plain|Boolean|false|按钮是否镂空，背景色透明|
|disabled|Boolean|false|是否禁用|
|loading|Boolean|false|名称前是否带 loading 图标|

## input
|属性名|类型|默认值|说明|
|--|--|--|--|
|value|String||输入框的初始内容|
|type|String|text|类型。text文本输入键盘、number数字输入键盘、idcard身份证输入键盘、tel电话输入键盘、digit带小数点的数字键盘 等|
|password|Boolean|false|是否是密码类型，H5和App写此属性时，type失效|
|placeholder|String||输入框为空时占位符|
|disabled|Boolean|false|是否禁用|
|maxlength|Number|140|最大输入长度，设置为 -1 的时候不限制最大长度|

## scroll-view
|属性名|类型|默认值|说明|
|--|--|--|--|
|scroll-x|Boolean|false|允许横向滚动|
|scroll-y|Boolean|false|允许纵向滚动|

## swiper
```js
<template>
    <swiper>
        <swiper-item>1</swiper-item>
    </swiper>
</template>
```
|属性名|类型|默认值|说明|
|--|--|--|--|
|indicator-dots|Boolean|false|是否显示面板指示点|
|indicator-color|Color|rgba(0, 0, 0, .3)|指示点颜色|
|indicator-active-color|Color|#000000|当前选中的指示点颜色|
|autoplay|Boolean|false|是否自动切换|
|interval|Number|5000|自动切换时间间隔|
|duration|Number|500|滑动动画时长|
|circular|Boolean|false|是否采用衔接滑动，即播放到末尾后重新回到开头|
|vertical|Boolean|false|滑动方向是否为纵向|

# easycom
安装在项目根目录的components目录下，并符合`components/组件名称/组件名称.vue`，无需在script下import引入、注册，直接在template中用组件标签使用即可

# 页面生命周期
1. `onLoad()` 页面加载时触发，可接收路由传参，适用于数据请求
2. `onShow()` 每次页面显示时触发，包括重新从其他页面返回
3. `onReady()` 页面第一次渲染完成后触发，此时可以安全操作视图 DOM
4. `onHide()` 页面隐藏（如跳转到其他页面）时触发
5. `onUnload()` 监听页面卸载
6. `onPageScroll(e)` 监听页面滚动，获取滚动位置 e.scrollTop
7. 等等

**不含组件的页面执行顺序**：onInit → onLoad → onShow → onReady

# rpx 尺寸单位
**概念**：响应式 px，一种根据屏幕宽度自适应的动态单位。以 750 宽的屏幕为基准

# 样式导入
```js
<style>
@import "../../common/uni.css";
</style>
```

# pages.json 页面路由
## pages 设置页面路径及窗口表现
```js
{
    "pages": [
        {
            "path": "pages/index/index",
            "style": { 
                "navigationBarTitleText": "index",
                // 是否开启下拉刷新
                "enablePullDownRefresh": false
            }
        }, {
            "path": "pages/login/login",
            "style": { ... }
        }
    ]
}
```
*注意：pages数组中的第一项表示应用启动页

## globalStyle 设置应用的状态栏、导航条、标题、窗口背景色等
```js
"globalStyle": {
    // 导航栏标题颜色及状态栏前景颜色，仅支持 black/white
    "navigationBarTextStyle": "white",
    // 导航栏标题文字内容
    "navigationBarTitleText": "我的uni-app项目",
    // 导航栏背景颜色（同状态栏背景色）
    "navigationBarBackgroundColor": "#007AFF",
    // 下拉显示出来的窗口的背景色，只适用于微信小程序
    "backgroundColor": "#F8F8F8",
    // 下拉 loading 的样式，仅支持 dark / light，只适用于微信小程序
    "backgroundTextStyle": "light",
    // 是否开启下拉刷新
    "enablePullDownRefresh": true,
    // 页面上拉触底事件触发时距页面底部距离，单位只支持px
    "onReachBottomDistance": 50
}
```
*注意：页面pages的设置权重高于globalStyle全局配置

## tabBar
```js
"tabBar": {
    "color": "#7A7E83",
    "selectedColor": "#3cc51f",
    "backgroundColor": "#ffffff",
    "borderStyle": "black",
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "首页",
        "iconPath": "static/images/tabBar/home.png",
        "selectedIconPath": "static/images/tabBar/home-active.png"
      },
      {
        "pagePath": "pages/category/category",
        "text": "分类",
        "iconPath": "static/images/tabBar/category.png",
        "selectedIconPath": "static/images/tabBar/category-active.png"
      }
    ]
}
```

# API 
## uni.showToast(OBJECT)
|参数|类型|必填|说明|
|--|--|--|--|
|title|String|是|提示的内容|
|icon|String|否|图标。success(默认)、error、fail、exception、loading、none|
|image|String|否|自定义图标的本地路径|
|mask|Boolean|否|是否显示透明蒙层，防止触摸穿透，默认false|
|duration|Number|否|提示的延迟时间，单位毫秒，默认1500|

```js
uni.showToast({
	title: '标题',
	duration: 2000
})
```

## uni.hideToast()
`uni.hideToast()` 隐藏消息提示框

## uni.showLoading(OBJECT)
显示 loading 提示框, 需主动调用 `uni.hideLoading()` 才能关闭提示框
|参数|类型|必填|说明|
|--|--|--|--|
|title|String|是|提示的内容|
|mask|Boolean|否|是否显示透明蒙层，防止触摸穿透，默认false|
|success|Function|否|接口调用成功的回调函数|
|fail|Function|否|接口调用成功的回调函数|

## uni.showModal(OBJECT)
|参数|类型|必填|说明|
|--|--|--|--|
|title|String|否|提示的标题|
|content|String|否|提示的内容|
|showCancel|Boolean|否|是否显示取消按钮，默认为 true|
|success|Function|否|接口调用成功的回调函数|
|fail|Function|否|接口调用成功的回调函数|

## uni.showActionSheet(OBJECT)
从底部向上弹出操作菜单
|参数|类型|必填|说明|
|--|--|--|--|
|title|String|否|菜单标题|
|itemList|Array<String>|是|按钮的文字数组|
|itemColor|HexColor|否|按钮的文字颜色，字符串格式，默认为"#000000"|
|success|Function|否|接口调用成功的回调函数|
|fail|Function|否|接口调用成功的回调函数|

```js
let arrs = ['A', 'B', 'C']
uni.showActionSheet({
	itemList: arrs,
	success: res => {
		console.log(arrs[res.tapIndex]);
	}
})
```
