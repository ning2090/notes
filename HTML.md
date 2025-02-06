# HTML 超文本标记语言

## 路径
- 相对路径：从 *当前文件位置* 出发查找目标文件（ ./当前文件夹下 ../当前文件夹的上一级文件夹）
- 绝对路径：从 *盘符* 出发查找目标文件

## 常用标签
1. 标题标签 \<h1> ~ \<h6>
2. 段落标签 \<p>
3. 换行标签 \<br>
4. 换行标签 \<hr>
5. 文本格式化标签
    |标签名|效果|
    |--|--|
    |strong|加粗|
    |em|倾斜|
    |ins|下划线|
    |del|删除线|
6. 图像标签 \<img>
    |属性名||
    |--|--|
    |src|路径|
    |alt|图片出不来时替换的文字|
    |title|鼠标移动到图片上时显示的文字|
7. 链接标签 \<a>
    |属性名||
    |--|--|
    |href|网址 #空连接 #id名可定位到页面某个位置|
    |target|打开窗口方式 _self当前窗口(默认) _blank新窗口|
8. 音频标签 \<audio>
    |属性名||
    |--|--|
    |src|路径|
    |controls|显示音频控制面板|
    |loop|循环播放|
    |autoplay|自动播放，浏览器一般禁用|
9. 视频标签 \<video>
    |属性名||
    |--|--|
    |src|路径|
    |controls|显示视频控制面板|
    |loop|循环播放|
    |muted|静音播放|
    |autoplay|自动播放，浏览器支持静音状态自动播放|
10. 无序列表
    ```html
    <ul>
        <li></li>
    </ul>
    ```
11. 有序列表
    ```html
    <ol>
        <li></li>
    </ol>
    ```
12. 定义列表
    ```html
    <dl>
        <dt>列表标题</dt>
        <dd>列表详情</dd>
    </dl>
    ```
13. 表格
    ```html
    <table>
        <thead>
            <tr>定义行
                <th>表头单元格</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>内容单元格</td>
            </tr>
        </tbody>
        <tfoot>
            ...
        </tfoot>
    </table>
    ```
    |属性名||
    |--|--|
    |align|对齐方式 left、center、right|
    |border|表格默认无边框线，通过该属性添加|
    |cellpadding|单元边沿与其内容间的空白，默认1像素|
    |cellspacing|单元格间的空白，默认2像素|
    |width|表格宽度|

    **合并单元格**
    1. 跨行合并：`rowspan = "合并个数"`
    2. 跨列合并：`colspan = "合并个数"`
14. 表单域 `<form action="url地址" method="提交方式" name="表单域名称">`
    - input标签 `<input type="类型">`
        |type属性值||
        |--|--|
        |text单行文本|placeholder="提示信息"|
        |password密码框|placeholder="提示信息"|
        |radio单选框|name="控件分组" checked默认选中|
        |checkbox多选框|checked默认选中|
        |file上传文件|multiple文件多选|
    - 下拉菜单
        ```html
        <select>
            <option>选项</option>
            <option selected>默认选中的选项</option>
        </select>
        ```
    - 文本域 `<textarea>默认提示文字</textarea>`
    - label标签：用来绑定文字和表单控件，增大表单控件的点击范围
        ```html
        // 写法一
        <input type="radio" id="man">
        <label for="man">男</label>

        // 写法二
        <label><input type="radio">女</label>
        ```
    - button按钮 `<button type="类型">按钮</button>`
        |type属性值||
        |--|--|
        |submit|提交按钮|
        |reset|重置按钮|
        |button|普通按钮|
15. 布局标签
    - div独占一行
    - span不换行
16. 字符实体
|显示结果|实体名称|
|--|--|
|空格|&nbsp;|
|小于号|&lt;|
|大于号|&gt|