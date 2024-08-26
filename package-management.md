# npm
**概念**：Node.js中的*第三方模块*又叫做*包*<br>
**来源**：不同于Node.js中的内置模块和自定义模块，包是由第三方个人或团队开发出来的，免费且开源<br>
**需要的原因**：由于Node.js的内置模块仅提供了一些底层的API，导致在基于内置模块进行项目开发时效率很低。包是基于内置模块封装出来的，提供了更高级、方便的API，提高开发效率<br>
**安装**：安装了node.js默认安装了npm<br>
**搜索包**：https://www.npmjs.com/<br>
**产生的文件**：
1. package.json包管理配置文件记录了项目的元数据信息以及项目所需的依赖包列表。<br>
（1）`npm i 包名` -> dependencies节点是开发和项目上线后都会用到的包<br>
（2）`npm i 包名 -D` = `npm install 包名 --save-dev` -> devDependencied节点是只在项目开发阶段用到的包
2. node_modules存放所有已安装到项目中的包
3. package-lock.json配置文件用来记录node_modules目录下每个包的下载信息

**命令**：
1. `npm -v` 查看npm包管理工具版本号
2. `npm init` 或 `npm init -y` 初始化一个新的npm项目，后面的命令用于自动填写npm init过程中所需的所有配置信息，使用默认值来生成package.json文件
3. `npm i 包名` 项目内安装包
4. `npm i 包名@版本号` 安装指定版本的包
5. `npm update 包名` 更新包到最新版本
6. `npm uninstall 包名` 卸载指定包
7. `npm i` 安装所有依赖包

## 下载包速度慢
**原因**：默认从国外的 https://registry.npmjs.org/ 服务器进行下载，此时，网络数据的传输需要经过漫长的海底光缆，因此下包速度会很慢<br>
**淘宝NPM镜像服务器**：

<img src="https://i-blog.csdnimg.cn/direct/839d27d08a3241d39da89327d8a7b310.png#pic_center" width="500px" />

*扩展：镜像是一种文件存储形式，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本即为镜像

**切换npm下包镜像源**：
1. `npm config get registry` 查看当前npm配置中使用的注册表地址
2. `npm config set registry XXX` 换成国内的源

## 包的分类
1. 项目包
    - 开发依赖包
    - 核心依赖包
2. 全局包：`npm i 包名 -g` 会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下，注意只有工具性质的包才有全局安装的必要性，因为它们提供了好用的终端命令，可以通过官网提供的使用说明判断需不需要全局安装。

<img src="https://i-blog.csdnimg.cn/direct/b345504e90e84c02ae4f932bb90220c9.png#pic_center" width="1000px" />

## i5ting_toc
**概念**：可以把md文档转为html页面的小工具<br>
**用法**：
1. `npm install -g i5ting_toc`
2. `i5ting_toc -f 要转换的md文件路径 -o`

# yarn
**安装**：`npm i -g yarn` 用npm全局安装yarn<br>
**命令**：
1. `yarn init` 初始化一个新的yarn项目
2. `yarn add 包名` 添加依赖包
3. `yarn upgrade 包名` 升级依赖包
4. `yarn remove 包名` 移除依赖包
5. `yarn` = `yarn install` 安装项目的全部依赖
