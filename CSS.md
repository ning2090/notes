# CSS 层叠样式表

## 引入方式
1. 内部样式表：style标签
2. 外部样式表：单独CSS文件中 `<link rel="stylesheet" herf="./my.css">`
3. 行内样式

## CSS特性
1. 继承性
2. 层叠性：相同属性后面的会覆盖前面的，不同属性都生效
3. 优先级：通配符选择器 < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important
    - 复合选择器叠加计算：(行内样式,id选择器个数,类选择器个数,标签选择器个数) 从左往右依次比较个数，同一级个数多的级别高，若相同则向后比较，!important权重最高，继承权重最低

## 选择器
- 基础选择器
    - 标签选择器
    - 类选择器：**.类名1 类名2**
    - id选择器：**#id名**
    - 通配符选择器：*
- 复合选择器
    - 后代选择器：**父选择器 子选择器{}**
    - 子代选择器：**父选择器>子选择器{}** 选中最近的子级
    - 并集选择器：**选择器1,选择器2{}**
    - 交集选择器：**选择器1选择器2{}** 如有标签选择器，则需写在最前面
- 伪类选择器
    - 鼠标悬停：**选择器:hover{}**
    - 超链接访问前：**选择器:link{}**
    - 超链接访问后：**选择器:visited{}**
    - 超链接点击时：**选择器:active{}**<br>
    注意：若给超链接设置以上四个状态，需按照LVHA的顺序书写
- 结构伪类选择器
    - 查找第一个E元素：**E:first-child**
    - 查找最后一个E元素：**E:last-child**
    - 查找第N个E元素(第一个元素N值为1，2n偶数，2n+1或2n-1奇数，n+5第5个以后的标签，-n+5第5个以前的标签)：**E:nth-child(N)**
- 伪元素选择器
    - 在E元素里最前面添加一个伪元素：**E::before**
    - 在E元素里最后面添加一个伪元素：**E::after**<br>
    注意：需设置`content:""`属性。伪元素默认行内显示模式，权重和标签选择器相同

## Emmet写法
**概念**：代码的简写方式，输入缩写自动生成对应代码
- HTML
    |说明|标签结构|Emmet|
    |--|--|--|
    |类选择器|`<div class="box"></div>`|标签名.类名|
    |id选择器|`<div id="box"></div>`|标签名#id名|
    |同级标签|`<div></div><p></p>`|div+p|
    |父子级标签|`<div><p></p></div>`|div>p|
    |多个相同标签|`<div>1</div><div>2</div><div>3</div>`|div*3|
    |有内容的标签|`<div>内容</div>`|div{内容}|
- CSS：大多数简写方式为属性单词的首字母

## 常见属性
### div属性
|属性名|效果|
|--|--|
|width|宽度|
|height|高度|
|background-color|背景色|

### 字体属性
|属性名|效果|
|--|--|
|font-size|字体大小|
|font-weight|字体粗细。400正常，700加粗|
|font-style|字体倾斜。normal正常，italic倾斜|
|line-height|行高。<br>形式一：数字+px  <br>形式二：数字 (当前字体大小的倍数)|
|font-family|字体族。多个字体名用逗号隔开|
|font|复合属性。是否倾斜 是否加粗 字号/行高 字体 (空格隔开)。字号和字体值必须书写，否则不生效|
|text-indent|文本缩进。<br>形式一：数字+px <br>形式二：数字+em (1em等于当前字号大小，即缩进两个字是2em)|
|text-align|对齐方式。left、center、right|
|text-decoration|修饰线。none无，underline下划线，line-through删除线，overline上划线|
|color|颜色。颜色关键字、rgb(r,g,b)、rgb(r,g,b,a)、#RRGGBB。其中a透明度取值0-1|

**单行文字垂直居中**：因为文字行高包含上下边距和文本高度，所以让 行高属性值等于盒子高度属性值 即可实现<br>
text-align本质是控制内容的对齐方式，属性要设置给内容的父级，例如想要让div中的图片居中显示，需要给div设置text-align:center

### 背景属性
|属性名|效果|
|--|--|
|background-color|背景色|
|background-image|背景图|
|background-repeat|平铺方式。no-repeat、repeat、repeat-x 水平方向平铺、repeat-y 垂直方向平铺|
|background-position|背景图位置。<br>形式一：水平方向位置 垂直方向位置 (left,right,center,top,bottom,若只写一个关键词，另一方向默认居中) <br>形式二：坐标 (数字+px，可正负，数字只写一个值表示水平方向，垂直方向为居中)|
|background-size|背景图缩放。<br>形式一：关键字 (cover等比例缩放图以完全覆盖，可能部分图会看不见；contain等比例完全装入背景区，可能部分背景区空白) <br>形式二：百分比 (根据盒子尺寸计算图片大小) <br>形式三：数字+单位|
|background-attachment|背景图固定。fixed 背景不会随元素内容滚动。|
|background|复合属性。背景色 背景图 平铺方式 位置/缩放 固定 (空格隔开，不区分顺序)|

## 显示模式
- 块级元素：常见有div、p、h1~h6等
    - 独占一行
    - 宽度默认是父级的100%
    - 添加宽高属性生效
- 行内元素：常见有span、a、img等
    - 一行共存多个
    - 宽高属性不生效
    - 宽高由内容撑开
- 行内块元素：常见有input、button等
    - 一行共存多个
    - 宽高属性生效
    - 宽高默认由内容撑开

### 转换显示模式
**属性名**：display<br>
**属性值**：
|属性值|效果|
|--|--|
|block|块级|
|inline-block|行内块|
|inline|行内|

## 盒子模型
- 内容区域 width & height
- 内边距 padding / padding-方位名词
    |padding多值个数|示例|含义|
    |--|--|--|
    |一个值|`padding:10px`|四个方向均为10px|
    |两个值|`padding:10px 20px`|上下10px，左右20px|
    |三个值|`padding:10px 20px 30px`|上10px，左右20px，下30px|
    |四个值|`padding:10px 20px 30px 40px`|上10px 右20px 下30px 左40px|
- 边框线 border：边框线粗细 线条样式 颜色（不区分顺序）<br> *单方向边框线* ：border-方位名词：边框线粗细 线条样式 颜色（不区分顺序）
    |线条样式属性值|效果|
    |--|--|
    |solid|实线|
    |dashed|虚线|
    |dotted|点线|
- 外边距 margin / margin-方位名词<br> *版心居中*：`margin:0 auto` 盒子要有宽度

**盒子尺寸 = 内容尺寸 + border尺寸 + 内边距尺寸**

不撑大盒子的解决方法：
1. 手动做减法：减掉border和padding的尺寸
2. 内减模式：`box-sizing:border-box`

### 元素溢出
**属性名**：overflow<br>
**属性值**：
|属性值|效果|
|--|--|
|hidden|溢出隐藏|
|scroll|无论是否溢出都显示滚动条位置（垂直和水平方向都有）|
|auto|溢出才显示滚动条位置|

### 圆角
**属性名**：border-radius<br>
**属性值**：数字+px 或 百分比(最大值是50%，超过50%没有效果)<br>
**常见应用**：
- 正圆形状：`border-radius:宽高的一半 或 50%;`
- 胶囊形状：`border-radius:高度的一半;`

### 阴影
**属性名**：box-shadow<br>
**属性值**：*X轴偏移量 *Y轴偏移量 模糊半径 扩散半径 颜色 内外阴影 (默认是外阴影，内阴影添加inset)

### 外边距问题——合并现象
**场景**：垂直排列的兄弟元素，上下margin会合并，取两个margin中的较大值生效

<img src="https://i-blog.csdnimg.cn/direct/6e598d14b920434ea9a65d262b6cb9fd.png#pic_center" width="600">

### 外边距问题——塌陷问题
**场景**：父子级的标签，子级添加上外边距会产生塌陷问题，也就是导致父级一起向下移动

<img src="https://i-blog.csdnimg.cn/direct/25ff768861594dc0b955d0ebd047fb1d.png#pic_center" width="600">

**解决方法**：
1. 取消子级 margin，父级设置 padding
2. 父级设置 `overflow:hidden`
3. 父级设置 border-top

### 行内元素——内外边距问题
**场景**：行内元素添加margin和padding，无法改变元素垂直位置<br>
**解决方法**：给行内元素添加line-height可以改变垂直位置

## 清除默认样式
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

li {
    list-style: none;
}
```

## PxCook像素大厨 
**概念**：是一款切图设计工具软件，支持PSD文件的文字、颜色、距离自动智能识别
- 开发面板（自动智能识别）
- 设计面板（手动测量尺寸和大小）

## 布局模式

### 标准流
**概念**：也叫文档流，指的是标签在页面中默认的排布规则

### 浮动
**作用**：让块元素水平排列<br>
**浮动后的特点**：
- 顶对齐
- 具备行内块特点
- 脱标
- 父级宽度不够，浮动的子级会换行

**属性名**：float<br>
**属性值**：
- left：左对齐
- right：右对齐

#### 清除浮动
**浮动可能导致的问题**：若父级没有高度，子级浮动无法撑开父级高度，可能会导致页面布局错乱<br>
**清除方法**：
1. 额外标签法：在父元素内容的最后添加一个块级元素，设置CSS属性 `clear:both`
2. 单伪元素法：在父元素添加类名clearfix并使用以下代码
    ```css
    .clearfix::after {
        content: "";
        display: block;
        clear: both;
    }
    ```
3. 双伪元素法 (推荐)：在父元素添加类名clearfix并使用以下代码。其中before解决外边距塌陷问题
    ```css
    .clearfix::before,
    .clearfix::after {
        content: "";
        display: table;
    }

    .clearfix::after {
        clear: both;
    }
    ```
4. 父元素添加CSS属性 `overflow:hidden`

### Flex
**概念**：也叫弹性布局，子元素可以自动挤压或拉伸。不会产生浮动布局中的脱标现象<br>
**用法**：`display:flex;`
|属性名|效果|
|--|--|
|justify-content|主轴对齐方式。center、space-between、space-around、space-evenly、flex-start从起点开始依次排序(默认)、flex-end|
|align-items|侧轴对齐方式 (给弹性容器设置)。stretch拉伸至铺满容器、center、flex-start、flex-end|
|align-self|某个弹性盒子侧轴对齐方式 (给弹性盒子设置)|
|flex-direction|修改主轴方向。row水平(默认)、column垂直、row-reverse水平从右往左、column-reverse垂直从下向上|
|flex|主轴方向弹性伸缩比。整数数字，表示占用父级剩余尺寸的份数|
|flex-wrap|弹性盒子换行。wrap换行、nowrap不换行(默认)|
|align-content|行对齐方式。center、space-between、space-around、space-evenly、flex-start、flex-end|

*注意：默认情况下，主轴方向尺寸靠内容撑开，侧轴默认拉伸

## 定位
### 相对定位
**用法**：`position:relative;`<br>
**特点**：
1. 参照物：自己原来的位置
2. 不脱标，占位
3. 标签显示模式特点不变

### 绝对定位
**用法**：`position:absolute;`<br>
**使用场景**：子绝父相<br>
**特点**：
1. 参照物：先找最近的已经定位的祖先元素，若所有祖先元素都没有定位则参考浏览器可视区
2. 脱标，不占位
3. 标签显示模式特点改变，宽高生效，具备了行内块的特点

**居中**：如弹窗
```css
img {
    position: absolute;
    // 水平和垂直边偏移50%
    left: 50%;
    top: 50%;
    // 向左、向上移动自身尺寸的一半
    transform: translate(-50%, -50%);
}
```

### 固定定位
**用法**：`position:fixed;`<br>
**使用场景**：元素的位置在网页滚动时不会改变<br>
**特点**：
1. 参照物：浏览器窗口
2. 脱标，不占位
3. 标签显示模式特点改变，宽高生效，具备了行内块的特点

### 堆叠层级z-index
**默认效果**：按照标签书写顺序，后来者居上<br>
**用法**：`z-index: 整数;` 默认是0，取值越大显示顺序越靠上

## 垂直对齐方式
**属性名**：vertical-align (给图片加这个属性)<br>
**使用场景**：图片和文字对齐<br>
**问题描述**：浏览器把行内块、行内标签当文字处理，默认按基线对齐，导致图片底下有空白，转块级`display:block;` 或 使用vertical-align 就可解决<br>
**属性值**：
|属性值|效果|
|--|--|
|baseline|基线对齐 (默认)|
|top|顶部对齐|
|middle|居中对齐|
|bottom|底部对齐|

<img src="https://i-blog.csdnimg.cn/direct/59947b134a614d2c8598eee29d33ef83.png#pic_center" width="450">

## 过渡transition
**属性**：`transition:过渡的属性 花费时间(s);` 过渡可以是具体的CSS属性也可以是all。设置给元素本身
```css
img {
    width: 200px;
    height: 200px;
    transition: all 1s;
}

/* 修改宽高尺寸，从左上角开始缩放 */
img:hover {
    width: 300px;
    height: 300px;
}
```

## 平面转换transform
**作用**：又叫2D转换，改变盒子平面内的形态(位移、旋转、缩放、倾斜)，一般配合过渡使用

<img src="https://i-blog.csdnimg.cn/direct/344d38317473430493ac469438311cba.png#pic_center" width="280">

**属性**：
- 平移：`transform:translate(X轴移动距离, Y轴移动距离);` <br>取值可 数字+px / 百分比(参照自身尺寸计算)<br>只写一个值，表示沿着X轴移动；<br>也可以单独设置 translateX() 或 translateY()
- 旋转：`transform:rotate(旋转角度);`<br>单位是deg<br>取值为正，顺时针旋转；取值为负，逆时针旋转
- 改变转换原点：`transform origin:水平原点位置 垂直原点位置;`<br>取值可 数字+px / 百分比 / 方位名词(left、top、right、bottom、center)<br>给元素本身添加
- 多重转换：`transform:translate() rotate();`<br>会以第一种转换形态的坐标轴为准，所以先平移再旋转
- 缩放：`transform:scale(X轴缩放倍数, Y轴缩放倍数);`<br>只写一个值，表示X轴和Y轴等比例缩放<br>取值大于1表示放大，小于1表示缩小
- 倾斜：`transform:skew();`<br>单位是deg

## 渐变
- 线性渐变
    ```css
    background-image: linear-gradient(
        渐变方向(可选。取值 to 方位名词 或 角度度数),
        颜色1 终点位置(可选，百分比),
        颜色2 终点位置,
        ...
    );  
    ```  
- 径向渐变
    ```css
    background-image: radial-gradient(
        半径(可以是2条，则为椭圆) at 圆心位置(数字+px / 百分比 / 方位名词),
        颜色1 终点位置,
        颜色2 终点位置,
        ...
    );  
    ```  

## 空间转换transform
**作用**：又叫3D转换，是从坐标轴角度定义的X、Y和Z三条坐标轴构成了一个立体空间，Z轴位置与视线方向相同

<img src="https://i-blog.csdnimg.cn/direct/979698a29fdf41098d9653603dfa7800.png#pic_center" width="280">

**属性**：
- 平移：`transform:translate3d(x, y, z);` <br>`transform:translateX();`<br>`transform:translateY();`<br>`transform:translateZ();`<br>取值可 数字+px / 百分比(参照自身尺寸计算)
- 旋转：`transform:rotateZ(旋转角度);`<br>`transform:rotateX(旋转角度);`<br>`transform:rotateY(旋转角度);`<br>单位是deg<br>取值为正，顺时针旋转；取值为负，逆时针旋转<br>左手法则——左手握住旋转轴，拇指指向正值方向，其他四指弯曲方向为旋转的正值方向，也就是取值为正<br>拓展：`transform:rotate3d(x, y, z, 角度度数);` 设置自定义旋转轴及旋转角度，其中x, y, z取值为0-1
- 缩放：`transform:scale3d(x, y, z);`<br>`transform:scaleX();`<br>`transform:scaleY();`<br>`transform:scaleZ();`<br>取值大于1表示放大，小于1表示缩小

## 视距perspective
**作用**：指定了观察者与Z=0平面的距离，为元素添加透视效果<br>
**透视效果**：近大远小、近实远虚<br>
**属性**：`perspective:视距;` 必须添加给直接父级，取值范围800-1200

## 立体呈现transform-style
**作用**：设置元素的子元素是位于3D空间中还是平面中<br>
**属性名**：transform-style<br>
**属性值**：
- flat：子级处于平面
- preserve-3d：子级处于3D空间

**呈现立体图形步骤**：
1. 父元素添加 `transform-style:preserve-3d;`
2. 子级定位
3. 调整子盒子的位置 (位移或旋转)

<img src="https://i-blog.csdnimg.cn/direct/d7edea3bdeff47cd88af639f3c5d8a72.png#pic_center" width="280">

## 动画animation
**对比过渡**：实现多个状态间的变化过程，动画过程可控 (重复播放、最终画面、是否暂停)。而过渡实现的是两个状态间的变化过程<br>
**步骤**：
1. 定义动画
    ```css
    // 形式一
    @keyframes 动画名称 {
        from {}
        to {}
    }

    // 形式二：这里的百分比是动画时长的百分比
    @keyframes 动画名称 {
        0% {}
        10% {}
        ...
        100% {}
    }
    ```
2. 使用动画 `animation:*动画名称 *动画时长 速度曲线 延迟时间 重复次数 动画方向 执行完毕时状态;` <br>取值不分顺序<br>若有两个时间值，第一个表示动画时长，第二个表示延迟时间

**属性**：
|属性名|作用|属性值|
|--|--|--|
|animation-name|动画名称||
|animation-duration|动画时长||
|animation-delay|延迟时间||
|animation-fill-mode|执行完毕时状态|forwards最后一帧状态、backwards第一帧状态(默认)|
|animation-timing-function|速度曲线|steps(数字)逐帧动画|
|animation-iteration-count|重复次数|infinite无限循环|
|animation-direction|动画执行方向|alternate反向|
|animation-play-state|暂停动画|paused暂停，通常在:hover中使用|

**多组动画**：
```css
animation:
    run 1s steps(12) infinite,
    move 3s linear forwards,
    ...
;
```

**案例—走马灯**：无缝动画原理就是复制开头图片到结尾位置 (图片累加宽度 = 区域宽度)。具体来说就是若有7张图片，div内能显示3张图片，就把第1、2、3张图片复制到第7张图片后面，然后设置动画 `animation:动画名称 时长 infinite linear`

**案例—逐帧动画**：
1. 准备显示区域：盒子尺寸与一张精灵小图尺寸相同
2. 定义动画：移动背景图 (移动距离 = 精灵图宽度)
3. 使用动画：steps(N)，N与精灵小图个数相同

## 透明度opacity
**作用**：设置整个元素(包括背景和内容)的透明度<br>
**属性名**：opacity<br>
**属性值**：
- 0：透明
- 1：不透明
- 0-1之间小数：半透明

## 光标类型cursor
**属性名**：cursor<br>
**属性值**：
|属性值|效果|
|--|--|
|default|箭头 (默认)|
|pointer|小手效果|
|text|工字形|
|move|十字光标|

## CSS精灵
**概念**：网页图片应用处理方式。把背景图片整合到一张图片文件中，再用background-position精确定位出背景图片的位置<br>
**作用**：减少服务器被请求的次数，减轻服务器的压力，提高页面加载速度<br>
**步骤**：
1. 创建盒子，尺寸与小图尺寸相同
2. 设置盒子背景图为精灵图
3. 添加background-position属性，改变背景图位置

## 字体图标
**概念**：展示的是图标，本质是字体<br>
**作用**：灵活、轻量级、兼容性、使用方便<br>
**图标库**：<a href="https://www.iconfont.cn/">https://www.iconfont.cn/</a><br>
**步骤**：
1. 在网站中添加需要的图标到项目中，下载并解压
2. 将整个包改名为iconfont，并拖入项目目录中
3. 引入样式表 `<link rel="stylesheet" herf="./iconfont/iconfont.css">`
4. 标签使用字体图标类名 `<span class="iconfont icon-xxx"></span>` icon-xxx从文件夹中的.html内复制
5. 修改样式
    ```css
    .iconfont {
        font-size: 200px;
        color: red;
    }
    ```

## 简单web
### 项目目录
- images文件夹
- uploads文件夹：非固定使用的图片素材，如商品图等
- iconfont文件夹
- css文件夹
    - base.css：基础公共样式
    - common.css：各个网页相同模块的重复样式，如头部、底部
    - index.css
- index.html

### SEO三大标签
**概念**：搜索引擎优化，提升网站百度搜索排名<br>
**网页头部SEO标签**：
1. title：网页标题标签
2. description：网页描述
3. keywords：网页关键字

<img src="https://i-blog.csdnimg.cn/direct/2cba3b8c0fe54281905529475c9bb289.png#pic_center" width="600">

### Favicon图标
**概念**：网页图标，出现在浏览器标题栏。favicon.ico，一般存放到网站根目录中

<img src="https://i-blog.csdnimg.cn/direct/093106adda4c438f8752415f0f0d62f3.png#pic_center" width="600">

### logo
**功能**：
1. 单击跳转到首页
2. 搜索引擎优化：提升网站搜索排名

**方法**：h1 > a > 网站名称
```css
.logo a {
    display: block;
    width: 100px;
    height: 100px;
    background-image: url(../image/logo.png);
    font-size: 0;
}
```

### nav
**方法**：ul > li > a 避免堆砌a标签，网站搜索排名降级<br>
**思路**：li设置右侧margin，a设置左右padding