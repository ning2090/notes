# 前端工程化
**概念**：开发项目直到上线，过程中集成的所有工具和技术（包括压缩工具、格式化工具、转换工具、打包工具、脚手架工具等）。而Node.js是前端工程化的基础，因为它可以主动读取前端代码内容

# Node.js
**概念**：Node.js是一个跨平台JavaScript运行环境，使开发者可以搭建服务器端的JavaScript应用程序。作用是使用它来编写服务器端程序，编写数据接口，提供网页资源浏览功能等；前端工程化，为框架做铺垫
**执行**：终端输入node xxx.js

<img src="https://i-blog.csdnimg.cn/direct/48b0b12fb3964096bb61eb89d5016e62.png#pic_center" width="800">

## fs模块—读写文件
**概念**：封装了与本机文件系统进行交互的，方法/属性
**语法**：
1. 加载fs模块对象 `const fs = require('fs')`
2. 写入文件内容
    ```js
    fs.writeFile('文件路径','写入内容',err => {
        if (err) console.log(err)
        else console.log('写入成功')
    })
    ```
3. 读取文件内容
    ```js
    fs.readFile('文件路径',(err, data) => {
        if (err) console.log(err)
        // data是文件内容的buffer数据流
        else console.log(data.toString())
    })
    ```

## path模块—路径处理
**问题**：Node.js代码中，相对路径是根据终端所在路径来查找的，可能无法找到想要的文件<br>
**建议**：Node.js代码中，使用绝对路径<br>
**补充**：__dirname内置变量，用来获取当前模块目录的绝对路径<br>
**概念**：path.join()会使用特定于平台的分隔符（例如windows和mac的目录分隔符不同），作为定界符，将所有给定的路径片段连接在一起<br>
**语法**：
1. 加载path模块 `const path = require('path')`
2. 使用path.join方法拼接路径，可以配合__dirname使用 `path.join(__dirname,'路径2',...)`

## http模块—创建Web服务
**需求**：创建本机Web服务并相应内容给浏览器<br>
**语法**：
```js
// 1.加载http模块，创建Web服务对象
const http = require('http')
const server = http.createServer()

// 2.监听request请求事件，设置响应头和响应体
server.on('request', (req, res) => {
   // 设置响应头：内容类型，普通文本；编码格式为utf-8
   res.setHeader('Content-Type', 'text/plain;charset=utf-8')
   res.end('欢迎使用node.js创建的Web服务')
})

// 3.配置端口号并启动Web服务，终端node xxx.js，并使用http://localhost:3000打开预览
server.listen(3000, () => {
    console.log('Web服务已启动')
})

// 若要使用req.url获取请求资源路径，读取index.html内的内容并返回给请求方，中间部分替换，其他不变终端node xxx.js，并使用http://localhost:3000/index.html打开预览
const fs = require('fs')
const path = require('http')
server.on('request', (req, res) => {
    if(req.url === '/index.html'){
        fs.readFile(path.join(__dirname, 'dist/index.html'),(err, data) => {
            if(err) console.log(err)
            else {
                res.setHeader('Content-Type', 'text/html;charset=utf-8')
                res.end(data.toString())
            }
        })
    } else {
        res.setHeader('Content-Type', 'text/html;charset=utf-8')
        res.end('你要访问的资源不存在')
    }
})
```

## 模块化
**概念**：在Node.js中，每个文件都被视为一个单独的模块，项目是由多个模块文件组成的，提高代码复用性，按需加载，独立作用域。需要使用标准语法（包括CommonJS标准和ECMAScript标准）导出和导入使用

### CommonJS标准
**语法**：
1. 导出 
    ```js
    module.exports = {
        对外属性名1：value1,
        对外属性名2：value2
    }
    ```
2. 导入 `require('模块名或路径')` （其中内置模块直接写模块名，自定义模块写文件路径）

### ECMAScript标准
**语法**：全部加载用默认导出和导入，按需加载用命名导出和导入
1. 默认导出 
    ```js
    export default = {
        对外属性名1：value1,
        对外属性名2：value2
    }
    ```
2. 默认导入 `import 变量名 from '模块名或路径'`
3. 命名导出 `export 修饰定义语句`
4. 命名导入 `import {同名变量} from '模块名或路径'`

*注意：Node.js默认支持CommonJS标准语法，如需使用ECMAScript标准语法，在运行模块所在文件夹新建package.json文件，并设置 `{"type":"module"}`