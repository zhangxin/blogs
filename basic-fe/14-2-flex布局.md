# FLEX

网页布局（layout）是 CSS 的一个重点，也是很多新人（包括我）很头疼的问题。在 Flex 布局到来之前，通常需要用很多种属性组合才能达到想要的效果。然而，CSS 各种属性组合之间互相影响，如果对文档流及各种定位机制了解的不够深入，很难做出理想的布局效果。Flex 属性到来之后，这一切都变得简单起来，这篇文章就介绍下这种全新的布局方法。

> css 各种属性之间相互影响见 [css不正交](https://zhuanlan.zhihu.com/p/29888231)
## 常见布局方式
- 固定宽度布局
- 弹性（fluid）布局
- 响应式布局 —— 多终端（PC、Pad、Phone）

### 布局实例
#### 单栏布局

   ![单栏布局](imgs/014/flex/一栏布局.png)
   - 一栏布局 [demo](http://js.jirengu.com/bazuz/2/edit?html,css,output)
   - 一栏布局(通栏) [demo](http://js.jirengu.com/rekur/1/edit?html,css,output)

#### 内部元素水平居中

   ![内部元素水平居中](imgs/014/flex/内部元素水平居中.png)
   - 一块居中[demo](http://js.jirengu.com/remew/1/edit?html,css,output)
   - 多块居中[demo](http://js.jirengu.com/parux/1/edit?html,css,output)
   - 多块居中(无间隙)
        - 用flex [demo](http://js.jirengu.com/kesam/1/edit?html,css,output)
        - 不用flex [demo](http://js.jirengu.com/dakek/1/edit?html,css,output)

#### 双列布局
   - 一列宽度固定，一列宽度自适应
   - [demo](http://js.jirengu.com/mogat/1/edit?html,css,output)

![双列布局.png](imgs/014/flex/双列布局.png)

#### 三列布局
   - 两侧两列固定宽度，中间列自适应宽度
   - [demo](http://js.jirengu.com/xicut/2/edit?html,css,output)
![三列布局.png](imgs/014/flex/三列布局.png)

#### 总结

![布局总结](imgs/014/flex/b2-1.gif)

在Flex之前，我们主要采用什么方式布局呢，主要是以下几种的组合：

1. normal flow（正常流，也叫普通流）
2. float + clear
3. position relative + absolute
4. display inline-block
5. 负margin

## Flex布局

2009 年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

- 特点
  1. 块级布局侧重于垂直方向，行内布局侧重于水平方向，flex 布局是**与方向无关**的
  2. flex 布局可以实现**空间自动分配，自动对齐**（flexible: 弹性，灵活）
  3. flex 适用于**简单的线性布局**，更复杂的布局应交给 grid 布局
      - [grid布局1](https://zhuanlan.zhihu.com/p/33030746)
      - [grid布局2](https://zhuanlan.zhihu.com/p/33031255)

- Flex 布局基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。


容器（container）默认存在两根轴：主轴（main axis）和侧轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做 `main start`，结束位置叫做 `main end`；侧轴的开始位置叫做 `cross start`，结束位置叫做 `cross end`。

项目默认沿主轴排列。单个项目占据的主轴空间叫做 `main size`，占据的交叉轴空间叫做 `cross size`。

- 共10个知识点，具体见下图



![flex布局基本概念.PNG](imgs/014/flex/flex布局基本概念.png)


与 Flex 布局相关的属性一共有 12 个，不要被吓到，其实很好明白。

首先是与容器（container）相关的6个属性：

### Flex Container 属性 
如下表所示，主要记四个（1 2 4 5）

|     属性名      |              作用               |
| :-------------: | :-----------------------------: |
| flex-direction  |          设置主轴方向           |
|    flex-wrap    |            是否换行             |
|    flex-flow    |         上面两个的简写          |
| justify-content |      主轴方向上的对齐方式       |
|   align-items   |  侧轴对齐方式，默认值 stretch   |
|  align-content  | 多行/列内容对齐方式（用的不多） |

#### 1. flex-direction

`flex-direction`属性决定主轴的方向（即项目的排列方向）。为什么说Flex布局与方向无关，就是因为该属性。它共有以下几个值：

```
row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。
```
![主轴方向](imgs/014/flex/b2-2.png)

#### 2. flex-wrap

因为 Flex 布局是空间自动分配，默认情况下当空间不足时，元素不会换行且会自动压缩，`flex-wrap` 属性决定了当空间不足时元素是否换行。它可能的取值有 3个。
1. `nowrap`（默认）：不换行。[图片上传中...(b2-5.jpg-a39120-1530119415668-0)]

![不换行](imgs/014/flex/b2-3.png)

2. `wrap`：换行，第一行在上方。

![换行，第一行在上方](imgs/014/flex/b2-5.jpg)

3. `wrap-reverse`：换行，第一行在下方。
![换行，第一行在下方](imgs/014/flex/b2-6.jpg)

#### 3. flex-flow
`flex-flow` 是上面两种属性的简写，如

```
.box {
  flex-flow: row wrap;
}
```

#### 4. justify-content

`justify-content` 属性定义了项目（items）在主轴方向的对齐方式，可能的取值有 5 个

```
1. flex-start（默认值）：左对齐
2. flex-end：右对齐
3. center： 居中
4. space-between：两端对齐，项目之间的间隔都相等。
5. space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```

#### 5. align-items 属性
`align-items` 属性定义项目（items）在侧轴上如何对齐。可能的取值有 5 个。

```
1. flex-start：侧轴的起点对齐。
2. flex-end：侧轴的终点对齐。
3. center：侧轴的中点对齐。
4. baseline: 项目的第一行文字的基线对齐。
5. stretch（默认值）：如果项目未设置高度或设为 auto，将占满整个容器的高度。items 的高度固定的话，align-items:stretch 不起作用
```

![侧轴对齐方式](imgs/014/flex/b2-7.png)

#### 6. align-content 属性
`align-content` 属性定义了多根轴线（即多行）的对齐方式。如果项目只有一根轴线，该属性不起作用。该属性用到的机会不多，了解即可。可能取值 6 个

```
1. flex-start：侧轴的起点对齐。
2. flex-end：侧轴的终点对齐。
3. center：与侧轴的中点对齐。
4. space-between：与侧轴两端对齐，轴线之间的间隔平均分布。
5. space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
6. stretch（默认值）：轴线占满整个侧轴。
```
![多根轴线（即多行）的对齐方式](imgs/014/flex/b2-8.png)

> `align-content` 和 `align-items` 属性容易混淆，我的理解是 `align-items` 控制所有元素在侧轴上整体的位置，所有元素会由于 `align-items` 值的改变步调一致的改变位置。而 `align-content` 控制的是行与行（假定主轴是横向的）之间位置的关系，每一行的位置会因为 `align-content` 值的改变而单独改变


接下来是项目（items）相关的属性

### Flex iteam 属性
  - 如下图所示，主要记（1,2,3,5,6）
![Flex item属性.png](imgs/014/flex/Flex item属性.png)

#### 1. flex-grow 属性

`flex-grow` 属性定义项目的放大比例，即存在剩余空间时，各个项目按照什么比例分配剩余空间，默认为 0，即如果存在剩余空间，也不放大。

![flex-grow属性](imgs/014/flex/b2-9.png)

#### 2. flex-shrink 属性
`flex-shrink`属性定义了项目的缩小比例，即空间不足时，各个项目按照什么比例缩小，默认为1，即如果空间不足，该项目将缩小。

![flex-shrink](imgs/014/flex/b2-10.jpg)

如果所有项目的 `flex-shrink` 属性都为 1，当空间不足时，都将等比例缩小。如果一个项目的 `flex-shrink` 属性为 0，其他项目都为 1，则空间不足时，前者不缩小。

#### 3. flex-basis 属性
`flex-basis` 属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为 auto，即项目的本来大小。

#### 4.flex 属性
`flex `属性是 `flex-grow`, `flex-shrink` 和 `flex-basis` 的简写，默认值为`0 1 auto`。后两个属性可选。


#### 5.align-self 属性
`align-self` 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 `align-items` 属性。默认值为 `auto`，表示继承父元素的 `align-items` 属性，如果没有父元素，则等同于 `stretch`。
可能的值有 6 个

```
auto | flex-start | flex-end | center | baseline | stretch;
```

![align-self](imgs/014/flex/b2-11.png)

#### 6. order 属性
`order` 属性定义项目的排列顺序。数值越小，排列越靠前，默认为 0。有了这个属性，彻底告别双飞翼布局和圣杯布局（这两个布局方式我基本上每次想写都要去查，从来记不住）

这篇博客大量参考了阮一峰老师的博客，很多图片都是直接拿来用。感谢阮一峰老师详细而又易懂的博客，下面附上链接：

- 阮一峰博客
  - [flex布局语法](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
  - [flex布局实例](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
- 其他参考
  - [css不正交](https://zhuanlan.zhihu.com/p/29888231)
  - [grid布局1](https://zhuanlan.zhihu.com/p/33030746)
  - [grid布局2](https://zhuanlan.zhihu.com/p/33031255)


