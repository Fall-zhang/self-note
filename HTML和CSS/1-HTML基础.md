

> Create by **Fall** on 2019-07-11
>Recently revised in 2022-04-30

# HTML5

> `HTML`指的是`Hyper Text Markup Language` 即超文本标记语言
>
> 超文本标记语言的意义：标记特定文本实现特定的效果

## 基础标签

> 标签分为双标签和单标签
>
> - 双标签：有开头，有结尾，比如：`<div></div>`、`<span></span>`
> - 单标签：单个标签，比如：`<img>`

### 注释

写法：`<!-- 注释内容  -->` 在浏览器渲染后的页面看不到，只能在代码中看到注释的内容

任何语言的注释都是这个意义：

- 把暂时不用的代码注释起来，方便以后使用（代码停靠）
- 对开发人员进行提示（代码提示）

### 基础标签

`div`：做一个区域划分的块

`contenteditable` 添加到 `div` 的属性中，可以编辑 `div` 里面的内容

`span`：对文字做内部修饰

> `div`：也是最基本的块样式。
>
> `span`：也是最基本的行内样式

### 标题与段落

标题是双标签：` <h1></h1>、<h2></h2>.....<h6></h6>` 六层标题

段落双标签：`<p></p>`

> 在一个网页中，`<h1>`标题最重要，并且一个`.html`文件中只能出现一次 h1 标签
>
> 双标签：有开头，有结尾

### 文本修饰标签

强调标签 ：`<strong></strong>`、`<em></em>`

区别：

- `strong ` 用来加粗，`em` 用来将字体改为斜体
- `strong` 的强调性质更强，`em` 的强调性质弱

上标和下标

- 下标：`<sub></sub>`
- 上标：`<sup></sup>`

删除文本和插入文本

- 删除文本：`<del></del>`
- 插入文本：`<ins></ins>`
- 标记文本：`<mark></mark>`
- 代码文本：`<code></code>`

`<br>`：用于文本换行

```html
<strong>强调标签</strong>
<em>斜体标签</em>

2的平方这样表示：2<sub>2</sub>
氧气的化学式：O<sup>2</sup>

<del>删除了内容</del>
<ins>一般是下划线修饰</ins>
<mark>做了标记，一般是更改背景</mark>
<code>console.log('fall')</code>
```

### 图片标签

`img`：单标签

- `src` : 引入图片的地址
- `alt` ：当图片出现问题的时候，可以显示文字信息进行提示
- `title` ： 鼠标悬停在图片上面的时候的提示信息
- `width、height `: 调节图片的大小

```html
<img src='ptha.jpg' alt="出错时的内容填充" title="提示信息">
```

`img` 标签中的 `src` 路径

- 相对路径：`"./xxx/xxx.jpg"`、`"../xxx/xxx.jpg"`
- 绝对路径：`"e:/xxx/xxx/xxx.jpg"` 或者是网络绝对路径：`https://blahblah.com`

### 链接标签

a 标签双标签：`<a></a>`

- `href` 属性：连接的地址
- target属性：可以改变连接的打开方式，
  - 默认值为 `_self`，在当前页面进行打开
  - 在其他页面打开`_blank`

base - >单标签在head中使用，进行网页的整体打开方式的编辑

```html
<a href='www.4399.com' target='_blank'>点击进入新的页面</a>
```

### 链接和锚点

锚点可以使用进行当前页面的跳转，跳转到该锚点处

两种方式：

- 使用 # + id 属性
- 使用 # + name 属性(name使用于`<a name=""></a>`)

### 列表标签

列表是用来展示一系列的数据，譬如下面的数据：

<ul>
	<li>苹果</li>
  <ul>
    <li>红富士</li>
    <li>金冠</li>
  </ul>
  <li>香蕉</li>
  <li>橘子</li>
</ul>
共有三类列表：

- 无序列表： `ul > li`  符合嵌套的规范，即 `ul` 内部嵌套 `li` 
- 有序列表：`ol > li `  一般使用较少，可以用无序列表进行替代
- 自定义列表：`dl > dd/dt`  `dt`（正常子节点显示） `dd`（本行开头多加一个制表符） 

## 特殊符号

| 写法     | 表示的符号     |
| -------- | -------------- |
| `&lt;`   | 左尖括号       |
| `&gt;`   | 右尖括号       |
| `&nbsp;` | 空格           |
| `&reg;`  | &reg;商标符号  |
| `&copy;` | &copy;版权符号 |

>  由于浏览器会将一部分代码识别，无法渲染，想要使用该符号需要使用这些格式
>
>  `&nbsp;` 因为浏览器只能识别文本中的一个空格，如果想添加空格，需要使用特殊写法

## 表格标签

> 详细的表格标签内容可以在 3.1 章查看。

表格是用来展示表格的数据。

- `table`：用于包裹表格
- `tr`：行，一个 `tr` 就是一行，放在 `table` 内
- `th`：加粗的（行），可以理解为 table head
- `td`：行中的数据，必须在 `tr` 标签内部
- `caption`：用于放置标题

> 有嵌套关系的，要符合嵌套规范



`table` 中的语义化标签：`tHead`、`tBody`、`tFoot`

注：语义化标签只有 `tBody` 可以在一个表格内出现多次，其它两个只能出现一次

水平对齐方式：样式中设置`align` ，值可以为`left,center,right`，

垂直对齐方式：`valign` ，`top,middle,bottom`

扩展——table表格标签的特殊属性：

- 添加边框单线：`border-collapse：collapse`
- 隐藏空单元格：`empty-cells: hide`
- 斜线分类 ：`border/rotate`
- 列分组：`colgroup/col`

<table>
  <caption>健康登记表</caption>
  <tHead>
    <tr>
      <th>身高</th>
      <th>体重</th>
      <th>长相</th>
      <th>偏好</th>
    </tr>
  </tHead>
    <tr>
    	<td>180</td>
      <td>79</td>
      <td>偏好</td>
      <td>打篮球，梳中分</td>
    </tr>
</table>

## 表单标签

> 详细的表格标签内容可以在 3.1 章查看。

表单，用于让用户填写内容的表单。

表单标签中包括的内容有：`form`、`input`、`textarea`、`select`、`label`

`textarea`：多行文本框

可以通过`resize: none` 更改属性使文本框不能调节大小

### select标签

下拉标签

```html
<select name="cars">
  <option name="cheap">奥拓</option>
  <option name="middle">大众</option>
  <option name="expensive">宾利</option>
  <option name="top">保时捷</option>
</select>
```

下拉菜单中如果select中添加`multiple='true'` 实现多选功能

<select name="cars">
	<option name="cheap">奥拓</option>
    <option name="middle">大众</option>
    <option name="expensive">宾利</option>
    <option name="top">保时捷</option>
</select>
### input标签

> 在元素内的可选属性
>
> `checked` 首次加载时选中
>
> `disabled` 选择不可用

| input 中 type 属性可选值 | 作用                               |
| ------------------------ | ---------------------------------- |
| radio                    | 定义圆形选择框（单选）             |
| checkbox                 | 方形选择框（复选框）               |
| button                   | 可定义按钮                         |
| file                     | 定义输入字段和上传按钮             |
| reset                    | 重置表单中的数据                   |
| submit                   | 可以把数据提交到服务器             |
| text                     | 单行的输入字段，默认宽度为20个字符 |
| hidden                   | 隐藏的输入字段                     |



