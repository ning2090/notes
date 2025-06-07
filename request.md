# url
**概念**：统一资源定位符，网址，用于访问服务器上资源<br>
**组成**：http://hmajax.itheima.net:80/api/province?name=wu&age=18<br>
1. http协议：超文本传输协议，规定浏览器和服务器之间传输数据的格式，协议范围http，https等
2. hmajax.itheima.net域名：标记服务器在互联网中方位
3. /api/provinc资源路径：标记资源在服务器下的具体位置
4. :80端口号：标记服务器里不同功能的服务程序，范围在0-65535之间的任意整数，默认访问80端口
5. ?name=wu&age=18查询参数：浏览器提供给服务器的额外信息

# 常见的服务程序
1. 80端口：Web服务（用于提供网上信息浏览功能）
2. 3000端口：Web服务
3. 8080端口：Web服务
4. 3306端口：数据库服务

*注意：0-1023和一些特定端口号被占用要避开使用

# 常用请求方法
**概念**：对服务器资源，要执行的操作
| 请求方法     | 操作     |
| -------- | -------- |
| GET | 获取数据 |
| POST | 提交数据 |
| PUT | 修改数据（全部） |
| DELETE | 删除数据 |
| PATCH | 修改数据（部分） |

# HTTP协议
**概念**：规定了浏览器发送及服务器返回内容的格式
## 请求报文
**概念**：浏览器按照HTTP协议要求的格式，发送给服务器的内容<br>
**组成**：
1. 请求行：请求方法，url，协议
2. 请求头：以键值对的格式携带的附加信息，如：Content-Type
3. 空行：分隔请求头，空行后是发送给服务器的资源
4. 请求体：发送的资源

<img src="https://i-blog.csdnimg.cn/direct/2ec9c2fdb6084b9babb3781a44165e09.png#pic_center" width="800">

## 响应报文
**概念**：服务器按照HTTP协议要求的格式，返回给浏览器的内容<br>
**组成**：
1. 响应行（状态行）：协议，HTTP响应状态码，状态信息
2. 响应头：以键值对的格式携带的附加信息，如：Content-Type
3. 空行：分隔响应头，空行后是服务器返回的资源
4. 响应体：返回的资源

<img src="https://i-blog.csdnimg.cn/direct/eb1a92469465412692b311cb566b451a.png#pic_center" width="400">

## 响应状态码
**概念**：用来表明请求是否成功完成
| 状态码  | 说明     |
| -------- | -------- |
| 1XX | 信息 |
| 2XX | 成功 |
| 3XX | 重定向消息 |
| 4XX | 客户端错误 |
| 5XX | 服务端错误 |

# 从浏览器地址栏输入url到显示页面的步骤
1. 浏览器根据请求的url交给DNS域名解析，找到真实IP
2. 建立TCP三次握手建立连接 (HTTPS还需TLS握手)
3. 服务器处理请求返回HTML，浏览器边解析边构建DOM树、渲染树
4. 绘制页面并加载子资源

# 向服务器请求数据的方法
1. 通过AJAX向服务器请求数据，本质就是使用XHR对象实现的
2. 通过axios实现，但底层仍然是基于XHR对象实现，本质不变，只是进行了promise的封装
3. Fetch API

# AJAX
**概念**：全称为Asynchronous JavaScript And XML，就是异步的JS和XML。通过AJAX可以在浏览器中向服务器发送异步请求，优势是无刷新获取数据。它不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式<br>
**优点**:
1. 无需刷新页面而与服务器端进行通信
2. 允许你根据用户事件来更新部分页面内容

**缺点**:
1. 没有浏览历史，不能回退
2. 存在跨域问题（同源）
3. SEO不友好

## XML
**概念**：是可扩展标记语言，被设计用来传输和存储数据。XML与HTML类似，但是XML中没有预定义标签，全部是自定义标签，用来表示一些数据。现在已经被JSON取代了
```js
// XML表示
<student>
    <name>吴</name>
    <age>18</age>
</student>
// JSON表示
{"name":"吴","age":18}
```

## Axios
**概念**：是一个基于Promise的HTTP客户端，用于浏览器和Node.js环境。它是Ajax技术的一种实现或封装，提供了HTTP请求方法。Axios封装了XMLHttpRequest的复杂性，使得发起HTTP请求和处理响应变得更加简单
```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>  
<script>  
    axios({
        url:'https://...',
        method:'请求方法，GET可省略',
        // GET请求查询参数
        params:{
            参数名：值
        }
        // POST请求提交数据
        data:{
            参数名：值
        }
    }).then(result => {
        // 处理数据
        console.log(result.data);
    }).catch(error => {
        //处理错误
    })
</script>
```

## XHR
**概念**：全称为XMLHttpRequest，用于与服务器交互。是axios的内部原理
```js
// 1. 创建XMLHttpRequest对象
const xhr = new XMLHttpRequest()
// 2. 配置请求方法和请求url地址
xhr.open('请求方法', 'url')
// 3. 监听loadend事件，接收响应结果
xhr.addEventListener('loadend', () => {
    console.log(xhr.response);
})
// 4. 发起请求
xhr.send()
```
### 查询参数
**语法**：`http://xxx.com/xxx/xxx?参数名1=值1&参数名2=值2`
### 数据提交
**语法**：
```js
const xhr = new XMLHttpRequest()
xhr.open('请求方法', 'url')
xhr.addEventListener('loadend', () => {
    console.log(xhr.response);
})
// 请求头设置传递数据的内容类型
xhr.setRequestHeader('Content-Type', 'application/json')
// 请求体数据并转成JSON字符串
const user = {username:'wu', password:'123'}
const userStr = JSON.stringify(user)
// 发送请求体数据
xhr.send(userStr)
```

# fetch
**概念**：内部采用promise方式来处理数据。采用了模块化设计，API分散于多个对象中，如Response对象、Request对象、Header对象。通过数据流（stream对象）处理数据，可以分块读取，利于提高网站性能
```js
// 方法1
fetch('http://...').then(res => {
    // 直接得到的res是一个Response对象，需要通过特定的方法获取其中的内容
    console.log(res)
    return res.json()
}).then(json => {
    // 由于res.json()返回一个Promise，需要再次使用then()来处理这个Promise解析后的结果
    console.log(json)
}).catch(err => {
    console.log(err);
})

// 方法2：封装成async异步函数（更常用）
async function getData(){
    try{
        let res = await fetch('http://...')
        let json = await res.json()
        console.log(json)
    }catch(err){
        console.log(err);
    }
}
getData()
```

## get请求设置查询参数
**语法**：`http://xxx.com/xxx/xxx?参数名1=值1&参数名2=值2`

## 配置参数
```js
async function getData(){
    let obj = {
        name:'wu',
        age:18
    }

    let res = await fetch('http://...',{
        method:'post',
        headers:{
            'Content-type':'application/json'
        },
        body:JSON.stringify(obj)
    })

    let json = await res.json()
    console.log(json)
}
getData()
```

## 了解Response对象
**概念**：fetch请求成功后，得到的是Response对象，它是对应服务器的HTTP响应<br>
**常见属性**：
| 属性     | 含义     |
| -------- | -------- |
| res.ok | 返回一个布尔类型，表示请求是否成功 |
| res.status | 返回一个数字，表示HTTP回应的状态码 |
| res.statusText | 返回状态的文本信息（例如请求成功后服务器返回ok） |
| res.url | 返回请求的url地址 |

**常见方法**：`res.json()`

# cookie
**概念**：是网站存储在用户浏览器中的小型文本数据，由键值对组成。用于维持状态（如登录）<br>
**查找**：可以右键检查 —> Application中找到cookie<br>
**获取**：`document.cookie`获取当前域名下的所有cookie (HttpOnly为ture的敏感数据无法获取)

<img src="https://i-blog.csdnimg.cn/direct/00c8a598902d46e18734c5f92f04904e.png#pic_center" width="700">

*注意不能跨浏览器读取cookie

<img src="https://i-blog.csdnimg.cn/direct/77264baed95e4fb4b34f3c31bd798aeb.png#pic_center" width="700">


# 网络请求跨域问题
**概念**：是由浏览器的同源策略（Same-Origin Policy）引起的，当请求的协议（http/https）、域名、端口任一不同时，浏览器会阻止请求<br>
**解决**：
1. CORS(后端才能解决)
2. Vite 配置（vite.config.js）
    ```js
    export default {
        server: {
            proxy: {
                <!-- 匹配所有以/api开头的请求路径 -->
                '/api': {
                    target: 'http://target-server.com',  // 目标服务器
                    changeOrigin: true,
                    pathRewrite: {'/api' : ''},
                },
            },
        },
    };
    ```
3. 等等