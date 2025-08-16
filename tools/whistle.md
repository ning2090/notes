# whistle
**概念**：本地代理工具，可以抓包、修改请求/响应、做调试和流量分析。相当于一个功能强大的本地代理服务器。可以通过浏览器访问 http://127.0.0.1:8899/ 查看抓包、修改请求等<br>
**安装**：
1. `npm install -g whistle`：全局安装（需要 Node.js 环境）
2. `w2 start`：启动 Whistle 服务

## 常用命令
1. `w2 stop`：结束服务
2. `w2 restart`：重启 Whistle 服务

## 常用操作界面
打开浏览器访问 http://local.whistlejs.com，主要界面和功能：
1. Rules（规则）：设置请求拦截、重定向、Mock 数据等规则。
    - Mock 接口数据
        ```bash
        /api/user   200   {"name":"Alice","age":20}
        ```
    - 重定向请求
        ```bash
        /api/login   https://test.example.com/login
        ```
    - 修改响应头/请求头
        ```bash
        header-set User-Agent:WhistleTest
        ```
2. History（历史）：查看经过 Whistle 的所有请求和响应，方便调试接口。
3. Plugins（插件）：安装额外插件扩展功能，比如 Mock、修改 Headers。


# SwitchyOmega
**概念**：浏览器插件，用来方便地切换浏览器代理，可以按规则选择不同代理<br>
**安装**：可以在浏览器应用商店内安装扩展程序<br>
**使用**：新建情景模式 → 设置自动切换规则(可选)