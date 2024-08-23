# 打包
**概念**：把静态模块内容（指的是html、css、js、图片等固定内容的文件），压缩，整合，转译等，包括*Webpack*、*Vite*、*Parcel*、*Rollup*、*Gulp*和*Grunt*

## Webpack
**概念**：静态模块打包工具<br>
**用法**：
1. 安装Webpack `npm i webpack webpack-cli --save-dev`
2. 配置局部自定义命令 `{"build":"webpack"}`
3. 运行 `npm run build` 命令，自动产生dist分发文件夹（压缩和优化后，用于最终运行的代码）

### 自动生成打包后html文件
**用法**：使用插件html-webpack-plugin
1. 下载插件 `npm i html-webpack-plugin --save-dev`
2. 配置webpack.config.js，具体操作查看官网文档

### 打包css代码
**概念**：因为Webpack默认只识别js代码，所以需要引入 `css-loader` 解析css代码和 `style-loader` 把解析后的css代码插入到DOM，具体操作见官网文档

### 提取css代码
**概念**：打包时css会存储在js模块中，想要提取css代码需要用到插件 `mini-cssextract-plugin` ，具体操作见官网文档。这样的好处是css文件可以被浏览器缓存，减少js文件体积<br>
*注意：不能和style-loader一起使用

### 压缩提取后的css代码
**概念**：css代码在提取后没有进行压缩，需要使用插件 `css-minimizer-webpack-plugin`，具体操作见官网文档

### 打包less代码
**概念**：加载器 `less-loader` 把less代码编译为css代码，具体操作见官网文档<br>
*注意：需要配合less软件包使用

### 打包图片
**概念**：Webpack5内置资源模块（字体，图片等）打包，无需loader<br>
**用法**：配置webpack.config.js让webpack拥有打包图片的功能，具体操作见官网文档。其中占位符[hash]对模块内容做算法计算，得到映射的数字字母组成的字符串；占位符[ext]使用当前模块原本的占位符，例如.png/.jpg等字符串；占位符[query]保留引入文件时代码中查询参数（只有URL下生效）<br>
*注意：判断临界值默认为8kb，大于8kb文件会发送一个单独的文件并导出url地址，小于8kb文件会导出一个data URL（base64字符串）

### 搭建开发环境
**概念**：之前改代码需要重新打包才能查看，现在通过配置 `webpack-dev-server` 快速开发应用程序<br>
**作用**：启动Web服务，自动检测代码变化，热更新到网页<br>
*注意：dist目录和打包内容是在内存里（更新快）<br>
**用法**：
1. 下载软件包 `npm i webpack-dev-server --save-dev`
2. webpack.config.js中设置模式为开发模式
    ```js
    module.exports = {
        //...
        mode: 'development'
    }
    ```
3. package.json中配置自定义命令 `"dev":"webpack server --open"`
4. 使用 `npm run dev` 来启动开发服务器

*注意：
1. webpack-dev-server借助http模块创建8080默认web服务
2. 默认以public文件夹作为服务器根目录
3. webpack-dev-server根据配置，打包相关代码在内存当中，以webpack.config.js下的output.path的值作为服务器根目录（所以可以直接拼接访问dist目录下内容）<br>
解决方案：在public文件夹下新建index.html，在script标签下加上 `location.href = '/login/index.html'` 就会自动跳转到首页

### 打包模式
**概念**：告知Webpack使用相应模式的内置优化<br>
**分类**：
| 模式名称 | 模式名字 | 特点 | 场景 |
| -------- | -------- |-------- |-------- |
| 开发模式 | development |调试代码，实时加载，模块热替换等 |本地开发 |
| 生产模式 | production |压缩代码，资源优化，更轻量等 |打包上线 |

**设置**：<br>
- 方式1：在webpack.config.js配置文件设置mode选项
    ```js
    module.exports = {
        //...
        mode: 'development'
    }
    ```
- 方式2：在package.json命令行设置mode参数
    ```js
    "scripts": {
        "build": "webpack --mode=production",
        "dev": "webpack serve --mode=developemt"
    }
    ```
*注意：命令行设置的优先级高于配置文件中的