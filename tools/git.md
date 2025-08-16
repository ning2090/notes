# git
## 操作流程
### push操作流程
 1. github上新建仓库
 2. 项目主目录下打开终端
 3. `git init`
 4. （可选）项目主目录下新建.gitignore文件，无后缀，将不是字符串的文件加进去，检测方法可采用用vscode打开查看是否是二进制文件，.gitignore文件内书写规范例：*.pyc
 5. （可选）LFS存放一些图片或表格等，能避免多次下载和上传图片等文件。步骤一：`git lfs install` 步骤二：`git lfs track *.png`
 6. `git add .`
 7. `git status` 注意LFS中存放的文件也会显示出来，.gitignore中忽略的文件不会加进去
 8. `git commit -m "first commit"`
 9. http步骤：根据github上的最后两步运行 步骤一：`git remote add origin ……` 步骤二：`git push……`
 
 另外`git reset`可重置  

### clone操作流程
 1. 下载git
 2. gitlab上复制http链接
 3. 新建文件夹，在目录下cmd，输入`git clone 链接`
 4. 创建分支，例如 ning/feature/change_doc
 5. `git status` 工作区文件当前状态
 6. `git add .` 添加所有修改的文件到暂存区
 7. `git commit -m "modified"` 提交到本地仓库
 8. `git push` 提交到远程仓库
### 冲突文件操作流程
 1. 切到主支上
 2. `git pull` 将主支更新到最新状态
 3. 切到冲突的分支上
 4. `git rebase master` 当前分支的更改应用到 master 分支的最新状态之上
 5. 有些冲突需要找到====的地方，手动选择accept both，再更改格式使其不报错
 6. `git add 冲突文件`
 7. `git rebase --continue` 继续rebase
 8. `git push --force` 由于进行了rebase操作，需要强制推送

## 命令
### git clone
`git clone 远程仓库的地址`  在当前目录下创建和版本库名相同的文件夹并下载版本到该文件夹下
`git clone 远程仓库的地址 本地目录`  指定目录下创建并下载版本到该文件夹下
### git init
`git init`  初始化本地仓库，在当前目录下生成 .git 文件夹
### git state
`git state`  查看本地仓库的状态
### git branch
`git branch`  查看当前分支
`git branch -a`  查看当前所有分支
`git branch 分支名`  创建新分支但没有切换过去
`git branch -D 分支名`  删除本地分支
### git checkout
`git checkout -b 分支名`  创建分支并切换过去
`git checkout 分支名`  切换分支
### git merge
`git merge 分支名`  把指定的分支合并到当前所在的分支下
### git push
`git push origin 分支名`  提交到指定分支
`git push 远程主机名 本地分支名:远程分支名`  提交到远程分支
`git push origin --delete 分支名`  删除远程分支
### git add
把要提交的文件的信息添加到暂存区中。当使用 git commit 时，将依据暂存区中的内容来进行文件的提交。
`git add 文件路径`  把指定的文件添加到暂存区中
### git commit
`git commit`  把暂存区中的文件提交到本地仓库，调用文本编辑器输入该次提交的描述信息
`git commit -m "提交的描述信息"`  把暂存区中的文件提交到本地仓库中并添加描述信息
`git commit --amend`  修改上次提交的描述信息
### git log
`git log`  打印所有的提交记录
### git pull
`git pull"`  更新本地仓库中的文件到最新的版本，这些最新版本是远程仓库中已存在的。实际执行了获取（fetch）和合并（merge）两个操作。
### git rebase
`git rebase master`  将当前分支的更改应用到 master 分支的最新状态之上。当提交的分支存在冲突文件时使用。会将当前分支的更改内容先放在临时区域内，剩下的部分会与master上最新提交合并，再将临时区域的内容合上来。有些冲突的代码，需要手动accept并修改格式。

## .gitignore
常见需要忽略的包和文件类型：
1. 依赖管理工具生成的文件和目录：
npm/yarn依赖：对于使用npm或yarn进行依赖管理的项目，通常会忽略node_modules/目录和package-lock.json/yarn.lock文件。node_modules/目录包含了项目的所有依赖包，它们通常体积庞大且会根据项目配置动态变化，因此不需要提交到仓库中。package-lock.json或yarn.lock文件用于锁定安装时的包的版本，以保证不同开发环境中依赖的一致性，虽然需要保留但通常由依赖管理工具自动生成。
Bower依赖（如果仍在使用）：对于使用Bower进行前端依赖管理的项目，会忽略bower_components/目录。
2. 编译生成的文件：
前端项目中使用各种构建工具（如Webpack、Gulp等）生成的文件，如打包后的JavaScript、CSS文件等，通常应该被忽略。具体文件类型取决于项目配置，但通常包括.js、.css、.map等后缀的文件，以及打包后可能生成的特定目录（如dist/、build/等）。
3. 编辑器配置文件：
不同编辑器和IDE生成的配置文件，如Visual Studio Code的.vscode/目录、WebStorm的.idea/目录等，这些文件包含了编辑器或IDE的特定设置，不需要被版本控制。
4. 日志文件和临时文件：
项目运行过程中产生的日志文件（如.log文件）和临时文件（如*.tmp文件）应该被忽略，以避免泄露敏感信息或增加仓库体积。
5. 本地配置文件：
包含敏感信息的本地配置文件（如数据库配置文件、API密钥文件等）应该被忽略，以确保敏感信息不会被提交到公共仓库。
6. 测试生成的文件：
测试运行过程中生成的文件或目录，如测试报告、覆盖率报告等，通常也不需要被版本控制。
7. 文档和构建输出：
对于一些自动化生成的文档（如使用JSDoc生成的API文档）和构建过程中的输出文件，也应该被忽略。
8. IDE项目文件：
某些IDE或开发环境可能会生成项目相关的文件或目录（如.project、.classpath等），这些文件特定于开发环境，不应该被版本控制。

以下是前端Web项目中常见需要忽略的文件和目录：
```
# 依赖  
/node_modules  
/bower_components  
  
# 编译生成的文件  
/dist  
/build  
*.js.map  
  
# 编辑器配置  
.vscode/  
.idea/  
  
# 日志和临时文件  
*.log  
*.tmp  
  
# 本地配置文件  
local_settings.json  
config/local.env  
  
# 测试相关  
/coverage  
*.coverage  
  
# 文档  
/docs/_build/  
  
# 其他  
*.iml  
*.o  
*.pyc  
*.swp  
*.swo  
*.tmp  
*.DS_Store  
*.user  
Thumbs.db
```

学习更多分支策略：https://juejin.cn/post/7217135786202251324
