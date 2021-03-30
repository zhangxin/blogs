# CSS 常见属性 上

text-align：用在块级元素上，对块级元素内的行内元素生效

## 块级元素和行内元素
### 块级元素

- block-level

```
div h1 h2 h3 h4 h5 h6 p hr
form ul dl ol pre table
li dd dt tr td th
```
### 行内元素

- 又称内联元素 inline-level

```
em strong span a br img 
button input label select textarea
code script
```

>  注意：input 默认为 inline-block

### 区别:

1. 块级元素占据一整行空间，行内元素占据自身宽度空间
2. 宽高属性的设置只对块级元素有效，对行内元素无效  

3. 块级元素可以包含块级元素和行内元素，行内元素只能包含文本和行内元素

4. 边距设置上有区别，块级元素可以设置四个方向的 margin padding，行内元素只能设置左右 margin 和 padding，设置上下 margin padding 是不生效的。内联元素在设置上下 padding 时，背景颜色和边框会被撑开，看起来像是上下 padding 生效了一样，其实元素本身的位置和并没有发生变化。

## CSS 属性继承

### 什么是 CSS 属性继承

被包在内部的标签拥有外部标签的样式性，即子元素可以继承父元素的样式

- 能继承的属性
	- 字体相关属性：font,font-family,font-weight,font-size,font-style,font-stretch,font-size-adjust
	- 文本相关属性：text-indent(文本缩进),text-align,line-height,word-spacing,letter-spacing,text-transform,direction,color
	- 元素可见性：visibility
	- 表格布局属:caption-side,border-collapse,border-spacing,empty-cells,table-layout
	- 列表布局属性：list-style-type,list-style-image,list-style-position,list-style
	- 生成内容属性：quotes
	- 光标属性：cursor
	- 页面样式属性：page,page-break-inside,window,orphans
	- 声音样式属性：speak,speak-punctuation….

- 不能继承的属性
	- display
	- 文本属性：vertical-align,text-shadow,text-decoration,white-space,unicode-bidi
	- 盒子模型相关属性：width,height,margin,border,padding
	- 背景相关属性：background,background-XXX
	- 定位属性：float,clear,position,top,right,bottom,left,min-width,min-height,max-width,max-height,overflow,clip,z-index
	- 生成内容属性：content,counter-reset,counter-increment
	- 轮廓样式属性：outline-style,outline=width,outline-color,outline
	- 页面样式属性：size,page-break-before,page-break-after
	- 声音样式属性：pause-before,pause-after,pause,cue-before,cue-after,cue,play-during

## 水平居中
- 块级元素居中：首先要给这个块级元素设置一个宽度,然后用 `margin: x auto`

- 行内元素居中：在块状元素内部用 `text-align: center`


## CSS 实现三角形

```css
selector {
  height:0;
  width:0px;
  border-top:solid 20px transparent;
  border-left:solid 20px transparent;
  border-right:solid 20px transparent;
  border-bottom:solid 20px blue;
}
```

## 单行文本溢出加 ...

```css
selector {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```
[测试](http://js.jirengu.com/corec/1/edit?html,css,output)

## 字体 font-family

### font-family 原理

使用浏览器打开页面时，浏览器会读取 HTML 文件进行解析渲染。当读到文字时会转换成对应的 unicode 码（可以认为是世界上任意一种文字的特定编号）。再根据 HTML 里设置的 font-family （如果没设置则使用浏览器默认设置）去查找电脑里（如果有自定义字体@font-face ，则加载对应字体文件）对应字体的字体文件。找到文件后根据 unicode 码去查找绘制外形，找到后绘制到页面上

### font-family 的写法

在 CSS 中设置字体时，直接写字体中文或英文名称浏览器都能识别，直接写中文的情况下编码（GB2312、UTF-8 等）不匹配时会产生乱码，还有一种意外情况是如果用户的操作系统没有中文，则即使有对应的字体也不能正常工作。保险的方式是将字体名称用 Unicode 来表示

宋体 | SimSun | \5B8B\4F53      黑体 | SimHei | \9ED1\4F53     微软雅黑 | Microsoft YaHei | \5FAE\8F6F\96C5\9ED1

打开控制台 `escape('微软雅黑')`，把 `%u`替换成 `\`

[字体原理 & iconfont 用法](https://zhuanlan.zhihu.com/p/22724856)

### font-family 实例

```css
body {
  font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;
}
```

- 作用
  - 设置文本样式，文本文字大小为 12px，文字所占行高为字体像素值的 1.5 倍。字体首选 tahoma，没有 tahoma 时选 arial，以此类推依次选择 'Hiragino Sans GB'，'\5b8b\4f53'，sans-serif
- 引号的作用
  - 某种字体的英文单词表达方式为多个单词时，用引号将它们括起来，避免被认为是多种字体
- \5b8b\4f53 代表黑体

## 文本属性

- text-align：文本对其方式 left、center、right、justify
- text-indent：文案第一行缩进距离
- text-decoration： none、underline、line-through、overline
- color：文字颜色
- text-transform：改变文字大小写none、uppercase、lowercase、capitalize
- word-spacing：可以改变字（单词）之间的标准间隔
- letter-spacing：字母间隔修改的是字符或字母之间的间隔

[范例](http://js.jirengu.com/riyu/1/edit)

### 单行文本溢出加 `...`

```css
.card > h3{
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

[demo](http://js.jirengu.com/dode/1/edit)

## 颜色

- 单词: `red`, `blue`, `pink`, `yellow`, `white`, `black`
- 十六进制: `#000000`, `#fff`, `#eee`, `#ccc`, `#666`, `#333`, `#f00`, `#0f0`, `#00f`
- rgb: `rgb(255, 255, 255)`, `rgb(0, 255, 0)`
- rgba: `rgba(0,0,0,0.5)`
- [更多](http://www.w3schools.com/colors/default.asp)

## 单位

- px：固定单位
- 百分比（宽高 文字大小 line-height  position）
- em: 相对单位，相对于父元素字体大小
- rem: 相对单位，相对于根元素 (html) 字体大小
- vw vh: 相对单位，1vw 为屏幕宽度的 1% [兼容性](http://caniuse.com/#search=vw)

## 隐藏 or 透明

元素在页面上不出现有三个层次：元素不在 DOM 中 ---> 元素在 DOM  中但是不在页面渲染，即不占用位置 ---> 元素在页面渲染但是是透明的，即看不到元素但是在页面中占用位置

|                                |                          |
| :----------------------------- | :----------------------- |
| `opacity: 0` ;                 | 透明度为 0，整体（包括子元素）会变透明 |
| `visibility: hidden` ;         | 和 opacity:0 类似             |
| `background-color: rgba(0，0，0，0.2)` | 只是背景色透明             |
| `display:none`; | 元素在页面消失，不占用位置 |

## a 链接设置颜色

a 有默认颜色和样式，会覆盖**继承**的样式。也就是说，如果不直接给 a 链接直接设置 color 而是给其父元素设置 color，那么 a 链接的颜色是不会变化的。

```css
a {
  color: red;
  text-decoration: none;
}
```
