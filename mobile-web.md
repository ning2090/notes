# 移动web

## 屏幕分辨率
**概念**：纵横向上的像素点数，单位是px
- 硬件分辨率 —> 物理分辨率 (出厂设置)
- 缩放调节的分辨率 —> 逻辑分辨率 (软件/驱动设置)

<img src="https://i-blog.csdnimg.cn/direct/e38f66f2975e44a09ff2d7f515bb5f33.png#pic_center" width="600">

## 视口
**概念**：显示HTML网页的区域，用来约束HTML尺寸
- 手机屏幕尺寸不同，网页宽度均为100%
- 网页的宽度和逻辑分辨率尺寸相同

<img src="https://i-blog.csdnimg.cn/direct/311081d31f6146c0a8cd3aef2a8d28c3.png#pic_center" width="600">

## 二倍图
**概念**：设计稿里面每个元素的尺寸的倍数<br>
**作用**：防止图片在高分辨率屏幕下模糊失真
- 现阶段设计稿参考iPhone6/7/8，设备宽度375px产出设计图，二倍图设计稿尺寸750px

## 适配方案
- 宽度适配：宽度自适应。适用PC端
    - 百分比布局
    - Flex布局
- 等比适配：适用移动端
    - rem
        - 相对单位，相对于HTML标签的字号计算结果。1rem = 1HTML字号大小
    - vw
        - 相对单位，相对于视口的尺寸计算结果。1vw = 1/100视口宽度。
        - vw和vh不能混用，推荐用vw
    - vh
        - 相对单位，相对于视口的尺寸计算结果。1vh = 1/100视口高度

### 媒体查询配合rem
**概念**：能检测视口的宽度，然后编写差异化的CSS样式。当某个条件成立，执行对应的CSS样式<br>
**特性**：
- max-width (因为存在层叠性，所以从大往小写)
- min-width (因为存在层叠性，所以从小往大写，如先min-width:100px，再min-width:200px)
```css
@media (媒体特性) {
    选择器 {
        CSS属性
    }
}

// 案例：目前rem布局方案中，HTML标签字号为视口宽度的1/10
@media (width:375px) {
    html {
        font-size: 37.5px;
    }
}
```
**完整写法(了解)**：`@media 关键词 媒体类型 and (媒体特性) {CSS代码}`
- 关键词/逻辑操作符
    - and
    - only
    - not
- 媒体类型
    - screen：屏幕
    - print：打印预览
    - speech：阅读器
    - all：包括以上3中情形(默认)
- 媒体特性
    - width、height
    - max-width、max-height
    - min-width、min-height
    - orientation：屏幕方向，属性值portrait竖屏、landscape横屏

**外部CSS**：
```css
<link rel="stylesheet" media="关键词 媒体类型 and (媒体特性)" href="xx.css">

// 案例：视口宽度小于等于768px，网页背景是粉色
<link rel="stylesheet" media="(max-width:768px)" href="./pink.css">
```

### rem—flexible.js
**概念**：是手机淘宝开发出的一个用来适配移动端的js库。核心原理是根据不同的视口宽度给网页中html根节点设置不同的font-size
```css
<body>
    ...
    <sccript src="./js/flexible.js"></sccript>
</body>
```

### rem—移动适配
**单位尺寸**：
1. 确定基准根字号：查看设计稿宽度 —> 确定参考设备宽度(视口宽度) —> 确定基准根字号(1/10视口宽度)
2. rem单位的尺寸 = px单位数值 / 基准根字号

**案例**：问题：计算68px是多少个rem？(设计稿适配375px视口)<br>
N * 37.5 = 68<br>
N = 68 / 37.5

### less
**概念**：是一个CSS预处理器，文件后缀.less。浏览器不识别less代码，所以目前网页要引入对应的CSS文件<br>
**VS Code插件**：Easy LESS，保存less文件后自动生成对应的CSS文件<br>
**运算**：
- 加、减、乘直接书写计算表达式
- 除法需要添加 小括号 或 .
    ```less
    .box {
        width: (68 / 37.5rem);
        height: 68 ./ 37.5rem;
    }
    ```
- 若表达式有多个单位，最终css里以第一个单位为准

**嵌套**：快速生成后代选择器
```less
.father {
    ...
    .son {
        ...
        a {
            color: green;
            // & 表示的是当前选择器，配合hover伪类或nth-child结构伪类使用
            &:hover {
                color: blue;
            }
        }
    }
}
```

**变量**：容器，存储数据，方便使用和修改
```less
// 1. 定义变量
@myColor: pink;

// 2. 使用变量
.box {
    color: @myColor;
}
```

**导入**：`@import "./base.less"` 导入less公共样式文件，less文件可以省略后缀<br>
**导出**：less文件第一行添加，若是文件夹名称后面添加/
```less
// out: ./index.css
// out: ./css/
```
**禁止导出**：less文件第一行添加 `// out:false`

### vw—移动适配
**单位尺寸**：
1. 确定设计稿对应的vw尺寸：查看设计稿宽度 —> 确定参考设备宽度(视口宽度) —> 确定vw尺寸(1/100视口宽度)
2. vw单位的尺寸 = px单位数值 / (1/100视口宽度)

## Bootstrap
**概念**：前端UI框架，提供大量编写好的CSS样式，能帮助快速编写功能完善的网页及常见交互效果<br>
**中文官网**：<a href="https://www.bootcss.com/">https://www.bootcss.com/</a><br>
**步骤**：
1. 官网下载生产文件
2. 将文件中的bootstrap.min.css复制到项目目录
3. 引入css文件 `<link rel="stylesheet" href="./css/bootstrap.min.css">`

### 栅格系统
**概念**：栅格化是指将网页的宽度分成12等份，每个盒子占用的对应的份数。具体看Bootstrap官网<br>
**常用布局类**：
- col-*-*：列 (例如col-xxl-3)
- row：行