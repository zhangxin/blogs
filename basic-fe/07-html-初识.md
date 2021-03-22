# HTML 初识

## HTML
超文本标记语言（Hypertext Markup language），是一种用于创建网页的标准标记语言，常与 CSS，JavaScript 一起用于设计网页、网页应用程序以及移动应用程序的用户界面。是语法较为松散的、不严格的 Web 语言，HTML 是一种标记语言而不是编程语言。

### HTML 的版本（W3C 组织制定规范）

HTML 最初由李爵士发明，后面不断加入新的标签。后来李爵士离开欧洲核子研究中心后创立 W3C（万维网委员会），专门负责写 HTML 的文档。HTML 逐渐形成规范。

i.   HTML 4.01

ii.   XHTML

iii.   HTML 5

iv.   HTML 5.1

### 规范文档（Specifications）

i.   由 W3C 写文档（李爵士创立）

ii.   W3C 根据浏览器的实际情况（即市面上主流浏览器支持哪些新标签）总结文档，并不是凭空想象

## XML
可扩展标记语言（Extensible Markup Language），主要用于存储数据和结构，不用来表现或展示数据。没有预定义标签，需要自己定义

## XHTML

可扩展超文本标记语言（eXtensible HyperText Markup Language，XHTML），基于 XML，作用与 HTML 类似，但语法更严格

## HTML语义化
语义化是一种编写 HTML 的方式，本质上是指在写页面的时候，选择合适的有意义的标签，使用合理的代码结构。即根据页面的结构（内容语义化），选择合适的标签（代码语义化）。比如善用 `header`，`main`，`aside` 等有意义的标签代替无意义的 `div`。

怎么使用合适的标签呢，有一个很好的方法，那就是记住标签对应的单词。基本上，知道标签对应单词的意思，就知道这个标签怎么用了（语义化）。比如 `a` 对应 `anchor`，当需要一个锚点或者超链接时候，很容易想到要使用 `a` 标签。

还有一个小技巧就是，判断页面上某处的内容是什么，比如是一个导航栏，是侧边栏等。搜对应意思的英文单词 + MDN，会很快找到合适的标签。比如搜索 navigation + mdn，就会搜到 `nav` 标签。所以学习 HTML 英语一定要好，必要的单词都得牢记于心。不要总是用 `div` 这种没有语义的标签。

好处：
1. 清晰的页面结构：去掉或样式丢失的时候，也能让页面呈现清晰的结构，增强页面的可读性。

2. 支持更多的设备：屏幕阅读器（如果访客有视障）会完全根据你的标记来“读”你的网页。 如果你使用的含语义的标记，屏幕阅读器会根据你的标签来判断网页的内容，而不是一个字母一个字母的拼写出来。

3. 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息，搜索引擎的爬虫也依赖于标记来确定上下文和各个关键字的权重。

4. 便于团队开发和维护：在团队中大家都遵循同一个标准，可以减少很多差异化的东西，方便开发和维护，提高开发效率，甚至实现模块化开发。


## 内容与样式分离
一个网页通常分为三个部分：HTML——内容和结构，CSS——样式，javascrip——行为。内容也就是 html，样式也就是 css。所以内容和样式的分离，就是指在网页编码的过程中，要将 html 和 css 两大部分分开。

- 写 HTML 的时候先不管样式, 重点放在 HTML 的结构和语义化上，让 HTML 能体现页面结构或者内容。之后再去写样式。

- 写 JS 的时候，尽量不要用 JS 去直接操作样式，而是通过给元素添加删除 class 来控制样式变化

- HTML 内不允许出现属性样式，尽量不要出现行内样式

优点:

1. 浏览器加载网页页面速度变快。分离原则下，关于样式的代码写在了 CSS 当中，页面体积容量变得更小。
2. 网页修改设计时，高效省时。根据 html 标签内 ID 或 class 的标记，到 CSS 里找到相应的选择器，可以快速替换指定位置的样式，不会破坏页面架构和其他部分的样式。典型的应用就是网页换肤，使用相同的 html 结构，不同的 css 样式。
3. 更好地被搜索引擎收录。基于内容与样式分离的原则，html 的语义化就是首要考虑的，网页中语义化的标签代码就会更加适合搜索引擎。
4. css 样式的分离，它可以根据不同的浏览器，达到显示效果的统一。保证网页架构不变形的前提下，放心在不同浏览器渲染显示样式。
## 常见 meta 标签
> meta 标签有四个属性，分别是 `name`，`http-equiv`，`charset`，`content`
- [常见meta标签](http://yunkus.com/meta-tag-usage/)

```html
<head>
<meta name="description" content="免费web教程">
<meta name="keywords" content="HTML,CSS,XML,JavaScript">
<meta name="author" content="W3Cschool">
<meta charset="UTF-8">
</head>
```
标签定义及使用说明
- 元数据（Metadata）是数据的数据信息。
- meta 标签提供了 HTML 文档的元数据。元数据不会显示在客户端，但是会被浏览器解析。
- meta 元素通常用于指定网页的描述，关键词，文件的最后修改时间，作者及其他元数据。
- 元数据可以被浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 Web 服务调用。

- 示例1
```html
定义文档关键词，用于搜索引擎：
<meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
```
- 示例2
```html
定义 web 页面描述：
<meta name="description" content="Free Web tutorials on HTML and CSS">
```
- 示例3
```html
定义页面作者：
<meta name="author" content="Hege Refsnes">
```
- 示例4
```html
每30秒刷新页面：
<meta http-equiv="refresh" content="30">
```
- 示例5
```html
屏幕的缩放
<meta name="viewport" content="">

content的几个属性：
    width viewport 的宽度 [device-width | pixel_value] width 如果直接设置pixel_value数值，大部分的安卓手机不支持，但是iOS支持；
    height – viewport 的高度 （范围从 223 到 10,000 ）
    user-scalable [yes | no]是否允许缩放
    initial-scale [数值] 初始化比例（范围从 > 0 到 10）
    minimum-scale [数值] 允许缩放的最小比例
    maximum-scale [数值] 允许缩放的最大比例
    target-densitydpi 值有以下（一般推荐设置中等像素密度或者低像素密度，后者设置具体的值dpi_value，另外webkit内核已不准备再支持此属性）
         -- dpi_value 一般是70-400//没英寸像素点的个数
         -- device-dpi设备默认像素密度
         -- high-dpi 高像素密度
         -- medium-dpi 中等像素密度
         -- low-dpi 低像素密度

完整案例:<meta name="viewport" content="width=device-width,height=device-height, user-scalable=no,initial-scale=1, minimum-scale=1, maximum-scale=1,target-densitydpi=device-dpi ">
```
- 示例6
```html
 声明文档使用的字符编码 
 <meta charset='utf-8'>
```
- 示例7
```html
设置作者姓名及联系方式
<meta name="author" contect="name, xxx@163.com" />
```
- 示例8
```html
声明文档兼容模式，指示IE以目前可用的最高模式显示内容
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"/>
```
## 文档声明
### 文档声明的作用
用来声明文档对象模型，用来告诉浏览器应该使用哪种方式来解析渲染页面。

### 严格模式和混杂模式
- 严格模式就是使用 `<!Doctype>` 标签来显式声明该用哪种方式来渲染页面
- 混杂模式即允许浏览器使用自己的方式来渲染页面。
### <!Doctype html> 的作用
- `<!Doctype html>` 就是声明使用HTML5来解析渲染页面。一般就用这种形式，因为其他的声明太难记了。。

## 浏览器乱码
浏览器乱码原因
- 文档保存时候的编码格式和浏览器解析时的解码格式不匹配导致的。
- 乱码一般是英文以外的字符才会出现。

如何解决

- 首先，在文件保存的时候你自己要清楚是用哪种编码方式保存的，然后在 html 文档中加入 `<meta charset="">` 标签，声明页面编码方式

## 常见的浏览器 & 内核
常见浏览器

- chrome，Firefox，ie，360，Safari、opera等

内核
1. Trident(IE内核)：IE 浏览器，很多国内浏览器，以及很多双核浏览器的其中“一核”都是 Trident。
2. Gecko：FireFox
3. Webkit：Chrome，Safari
4. Presto：Opera

## HTML 常见标签
|              常见标签              | 场景                                                         |
| :--------------------------------: | :----------------------------------------------------------- |
|           `<h1>...</h1>`           | 表示标题,h1到h6分别代表六级标题                              |
|            `<p>...</p>`            | 段落，表示大段文字                                           |
|            `<a>...</a>`            | 链接，链接到下一个地址，有`href`,  `target`,`title`三个属性,分别表示链地址（或#锚点，#about，/路径），页面打开方式，网页标题 |
|              `<img>`               | 展示图片，属性`src`：图片地址，属性`alt`:描述图片的注释。ps:只闭合标签，最后不需要 / |
|          `<div>...</div>`          | 表示一大块，用于给页面划分区域，让结构更清晰。属性：`id`,表示给一个元素取名；`class`:表示给一类元素取名 |
|           `<ul>...</ul>`           | 无序列表，用于表示并列的内容，`ul`的直接子元素是`li`,可以嵌套 |
|           `<ol>...</ol>`           | 有序列表                                                     |
|           `<li>...</li>`           | 列表项，与`ul`,`ol`结合使用                                  |
| `<dl>.</dl>` `<dt>.</dt>` `<dd>.</dd>` | 用于展示一系列 “标题:内容... ”的场景。description list---dl。description term---dt 。description definition---dd |
|      `<button>点我</button>`       | 按钮                                                         |
|  `<strong>.</strong> <em>.</em>`  | `em` 需要强调一下`strong` 很重要、强调性更强                 |
|         `<span>...</span>`         | 给某个需要加样式的元素添加标记，无强调语义                   |
|       `<iframe>...</iframe>`       | 用于嵌入一个页面。有两个属性，分别是 src 和 name。src 表示页面的地址，name 表示页面名称，可以和 `<a>` 标签的 target 属性配合 |
|        `<table>..</table>`         | 用于展示表格，不要用来做布局，`thead tbody tfoot`可省略      |
|           `<tr>..</tr>`            | 行，与`<table>..</table>`一起用于展示表格                    |
|           `<th>..</th>`            | 标题的列                                                     |
|           `<td>..</td>`            | 内容的列                                                     |
|         `<!Doctype html>`          | 文档对象模型                                                 |
|               `<br>`               | 换行                                                         |
|               `<hr>`               | 添加分割线                                                   |
|         `<html>..</html>`          | 整个页面的根节点，一个页面只能有一个 `<html>` 标签，所有内容应位于 `<html>` 标签内 |
|         `<head>..</head>`          | 用于定义文档的头部信息，它是所有头部元素的容器               |
|        `<title>...</title>`        | 文档的标题                                                   |
|         `<meta>...</meta>`         | 提供有关页面的元信息                                         |
|         `<body>...</body>`         | 文档的内容,即可视页面内容                                    |
| `nav` | 导航栏 |
| `header` | 头部 |
| `main` | 主要内容 |
| `footer` | 尾部 |
常见标签还有 kbd、video、audio、svg 等

> HTML 中，除了 `<span>` 标签和 `<div>` 标签，其他的标签都是有语义的。`<span>` 标签和 `<div>` 标签是没有实际语义的标签，所以一般使用时候要加上 class，不然就是含无意义的划分区块而已。

### 省略标签

注意：HTML 的 html head body 标签都可以省略，具体规则搜 html spec，官方文档里找，其实一般都会写上，写这点只是为了装，感觉很多人应该不知道。验证一个html 语法是否合法，可以搜 w3c html 验证器，会告诉你哪个地方有语法错误。

## 块级元素和内联元素

HTML 是没有块级元素和内联元素的区别的，也就是说没有哪个元素一定是块级元素或者内联元素。在 CSS 里面才会看块级元素和内联元素的区别。比如一般认为 div 是块级元素，但是如果将 div 的样式设置成为 in-line，那它就变成内联元素了。事实上，HTML 是不管样式的，无法控制一个元素是块级元素还是内联元素，HTML 只做一件事情，那就是定义某处的内容是什么东西，比如是一个标题，链接，段落等等，这就是常说的语义化。至于通常说块级元素、内联元素等，实际上是因为标签都有默认样式
