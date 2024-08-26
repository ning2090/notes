# 打包
**概念**：把静态模块内容（指的是html、css、js、图片等固定内容的文件），压缩，整合，转译等，包括*Webpack*、*Vite*、*Parcel*、*Rollup*、*Gulp*和*Grunt*

## Webpack
**概念**：静态模块打包工具<br>
**用法**：
1. 安装Webpack `npm i webpack webpack-cli --save-dev`
2. 配置局部自定义命令 `{"build":"webpack"}`
3. 运行 `npm run build` 命令，自动产生dist分发文件夹（压缩和优化后，用于最终运行的代码）

### Webpack.config.js
**概念**：Webpack.config.js是 Webpack 的配置文件，它告诉 Webpack 如何打包你的应用程序<br>
**常见组成**：
```js
module.exports = {  
    // 打包模式
    mode: 'development',
    // 入口
    entry: '', 
    // 出口
    output:{},
    // 插件（给webpack提供更多功能）
    plugins:[],
    // 加载器（让webpack识别更多模块文件）
    module:{},
    // 优化
    optimization:{},
    // 解析
    resolve:{},
}
```

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

### webpack环境下区分两种模式
**需求**：
- 开发模式：style-loader内嵌css代码在js中，让热替换更快
- 生产模式：提取css代码，让浏览器缓存和并行下载js和css文件
**方法**：
- 方法1：webpack.config.js配置导出函数，但是局限性大（只接受两种模式）
- 方法2：借助cross-env（跨平台通用）包名令，设置参数区分环境
    - 步骤1：下载cross-env软件包，具体操作见官网文档
    - 步骤2：配置自定义命令，传入参数名和值到process.env对象上（它是Node.js环境变量）
    - 步骤3：在webpack.config.js调用使用做判断区分
- 方法3：配置不同的webpack.config.js（适用多种模式差异性较大情况）

### 前端注入环境变量
**需求**：前端项目中，开发模式下打印语句生效，生产模式下打印语句失效<br>
**问题**：cross-env设置的只在Node.js环境生效，前端代码无法访问process.env.NODE_ENV<br>
**解决**：使用webpack内置的 `DefinePlugin` 插件，具体操作见官网文档。它能在编译时，将前端代码中匹配的变量名，替换为值或表达式

### 开发环境调错
**问题**：代码被压缩和混淆，无法正确定位源代码位置（行数和列数）<br>
**解决**：使用 `source map` 可以准确追踪error和warning在原始代码的位置<br>
**设置**：webpack.config.js配置devtool选项
```js
module.exports = {
    // ...
    // inline-source-map选项把源码的位置信息一起打包在js文件内
    devtool: 'inline-source-map'
}
```
*注意：source map仅适用于开发环境，不要在生产环境使用（防止被轻易查看源码位置）

### 解析别名 alias
**解析别名概念**：配置模块如何解析，创建import引入路径的别名，来确保模块引入变得简单<br>
**解决**：在webpack.config.js中配置解析别名@来代表src绝对路径
```js
module.exports = {
    // ...
    resolve:{
        alias:{
            '@': path.resolve(__dirname, 'src')
        }
    }
}
```

### 优化—CDN使用
**CDN概念**：内容分发网络，指的是一组分布在各个地区的服务器。能把静态资源文件/第三方库放在CDN网络中各个服务器中，供用户就近请求获取，能减轻自己服务器请求压力，就近请求物理延迟低，配套缓存策略

<img src="https://i-blog.csdnimg.cn/direct/752ad586843048aaa278ffe35a6e67f1.png#pic_center" width="800">

**需求**：开发模式使用本地第三方库，生产模式下使用CDN加载引入<br>
**用法**：
1. 在html中引入第三方库的CDN地址并用模板语句判断，具体操作见官网文档
    ```js
    <% if(htmlWebpackPlugin.options.useCdn){ %>
        <link herf="https://..." rel="stylesheet">
    <% } %>
    ```
2. 配置webpack.config.js中externals外部扩展选项（防止某些import的包被打包）
    ```js
    const config = {
        // ...
        plugins:[
            new HtmlWebpackPlugin({
                // 自定义属性，在html模板中访问使用
                useCdn:process.env.NODE_ENV === 'production'
            })
        ]
    }

    if(process.env.NODE_ENV === 'production'){
        config.externals = {
            // key：代码中import from 后面的模块标识字符串
            // value：替换在原地的变量名（要和cdn暴露在全局的变量名一致）
            'axios':'axios'
        }
    }
    ```

### 多页面打包
**单页面概念**：单个html文件，切换DOM的方式实现不同业务逻辑展示<br>
**多页面概念**：多个html文件，切换页面实现不同业务逻辑展示<br>
**用法**：
1. 准备源码（html、css、js）放入相应位置，并改用模板化语法导出，具体操作见官网文档
2. 下载form-serialize包并导入到核心代码中使用
3. 配置webpack.config.js多入口和多页面的配置

### 优化—分割公共代码
**需求**：把2个以上页面引用的公共代码提取<br>
**用法**：配置webpack.config.js的*splitChunks*分割功能，具体操作见官网文档

## Vite
**概念**：Vite是一个新型的前端构建工具，专为现代JavaScript应用程序而设计。它旨在提供快速的开发和构建速度，并通过利用浏览器原生支持的ES模块（ECMAScript Modules）特性来实现<br>
**配置文件**：vite.config.js<br>
**命令**：
- `npm create vite@latest` 使用命令构建项目，会自带vite包
- `npm i -D vite` 安装vite包
- `npm vite` 启动开发服务器，并没有对代码进行打包
- `npm vite build` 打包
- `npm vite preview` 启动服务器，预览的是打包后的代码

*注意：html中用script标签引入js文件需要加 `type="module"`