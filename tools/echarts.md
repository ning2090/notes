# echarts
**概念**：Echarts是有一款由百度前端技术开发的，基于javascript开发的一种数据可视化的图表库，能够提供直观、生动可交互可个性数据可视化图标

## 安装
`npm install echarts --save`
## 引入 ECharts
`import * as echarts from 'echarts';`

## 常见配置项 (option)
**概念**：ECharts 图表通过 option 对象进行配置

### title 标题
```js
title: {
  text: "主标题",
  subtext: "副标题",
  left: "center", // 控制水平方向位置
  top: "center", // 控制垂直方向位置
  textStyle: {
    color: 'black', //标题颜色
    fontSize: '16', //标题大小
  },
}
```

### legend 图例
```js
legend: {
  data: ["销量", "库存"],
  itemWidth : 15, //图例标记的图形宽度
  itemHeight : 15, //图例标记的图形高度
}
```

### grid 网格布局
**概念**：图表距离四周多少，相当于css中的padding
```js
grid: {
  left : '15%',
  right: '15%',
  top : '16%',
  bottom: '15%',  
}
```

### xAxis X轴
```js
xAxis: {
  name: '件', //单位
  type: "category", // 坐标轴类型。'value' 数值轴; 'category' 类目轴，适用于离散的类目数据; 'time' 时间轴; 'log' 对数轴
  data: ["Mon", "Tue", "Wed", "Thu", "Fri"]
}
```

### yAxis Y轴
**概念**：Y 轴是数值轴，ECharts 会根据你 series.data 的实际数值，自动计算并生成刻度范围和间隔
```js
yAxis: {
  name: '件', //单位
  type: "value",
}
```

### series 系列数据
```js
series: [
  {
    name: "销量",
    type: "bar", // 常见的 type：line(折线)、bar(柱状)、pie(饼图)、scatter(散点)、radar(雷达)、map(地图)
    barMinWidth: 10,  // 柱子最小宽度（像素）
    barMaxWidth: 50   // 柱子最大宽度（像素）
    barWidth : 20, // 设置柱状固定宽度
    data: [5, 20, 36, 10, 10]
  },
  {
    name: "趋势",
    type: "line",
    data: [2, 18, 30, 8, 12]
  }
]
```

### tooltip 提示框
```js
tooltip: {
  trigger: "axis", // 触发类型。'axis' 表示整个坐标轴提示; 'item' 数据项图形触发，表示悬浮点提示
  // 自定义提示内容
  formatter: params => {
    return params.map(item => `${item.marker}${item.seriesName}: ${item.value}`).join('<br/>');
  }
}
```

### color 颜色
**概念**：控制 series 的默认颜色（顺序分配）
```js
color: ['#a9abff','#ff8896'],
```

### dataZoom 区域缩放
```js
dataZoom: [
  {
    type: "slider" | "inside", // "slider" 显示一个可拖拽的滑块; "inside"内置交互（滚轮缩放、拖拽平移）
    xAxisIndex: 0,   // 作用在哪个 X 轴（0 表示第一个）
    yAxisIndex: 0,   // 如果是垂直方向，就绑定 Y 轴
    start: 0,        // 数据窗口范围起始（0%）
    end: 100,        // 数据窗口范围结束（100%）
  }
]
```

*拖动滑块* 或者 *鼠标滚轮/拖拽* 都可以控制x轴缩放:
```js
dataZoom: [
  {
    type: 'inside',
    xAxisIndex: 0
  },
  {
    type: 'slider',
    xAxisIndex: 0
  }
]
```


