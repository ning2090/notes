# nvm
**概念**：是一个 Node.js 版本管理工具，用来安装、切换和管理多个 Node.js 版本

## 常用命令
1. `nvm ls`：查看已安装的 Node.js 版本
2. `nvm install xx.xx.x`：安装指定版本 Node.js 
3. `nvm uninstall xx.xx.x`：卸载指定版本 Node.js 
4. `nvm use xx.xx.x`：切换版本，`node -v` 会显示对应版本

## 示例
```bash
$ nvm use 16
Now using node v16.9.1 (npm v7.21.1)

$ node -v
v16.9.1

$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)

$ node -v
v14.18.0
```