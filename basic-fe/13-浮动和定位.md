# 浮动定位 & BFC & 边距合并

## 浮动

浮动模型是一种可视化格式模型，浮动的框可以左右移动（根据float属性值而定），直到它的外边缘碰到包含框（padding 内侧）或者另一个浮动元素的框的边缘。浮动元素脱离了文档的普通流，普通流中的元素表现的就像浮动元素不存在一样。下面的代码可以直接复制到 jsbin 运行，就不贴具体的效果图了。动手运行比多少语言都讲得明白。

1. **正常情况**

```html
 <div style="border: solid 5px #0e0; width:300px;">
    <div style="height: 100px; width: 100px; background-color: Red;">
    </div>
    <div style="height: 100px; width: 100px; background-color: Green; ">
    </div>
    <div style="height: 100px; width: 100px; background-color: Yellow;">
    </div>
  </div>
```

2. **红向右浮动**

```html
<div style="border: solid 5px #0e0; width:300px;">
  <div style="height: 100px; width: 100px; background-color: Red; float:right;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Green; ">
  </div>
  <div style="height: 100px; width: 100px; background-color: Yellow;">
  </div>
</div>
```

3. **红框左移,覆盖绿框**

```html
<div style="border: solid 5px #0e0; width:300px;">
  <div style="height: 100px; width: 100px; background-color: Red;  float:left;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Green;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Yellow;">
  </div>
</div>
```

4. **都向左浮动,父元素宽度为0**

```html
<div style="border: solid 5px #0e0; width:300px;">
  <div style="height: 100px; width: 100px; background-color: Red;  float:left;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Green;  float:left;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Yellow;  float:left;">
  </div>
</div>
```

5. **包含块儿太窄**

> 如果包含块儿太窄无法容纳水平排列的三个浮动元素,那么其它浮动块儿向下移动,直到有足够的空间,如果浮动元素的高度不同,那么向下移动的时候可能被卡住

```html
<div style="border: solid 5px #0e0; width:250px;">
  <div style="height: 100px; width: 100px; background-color: Red;  float:left;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Green;  float:left;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Yellow;  float:left;">
  </div>
</div>
```

6. **卡住**

```html
<div style="border: solid 5px #0e0; width:250px;">
  <div style="height: 120px; width: 100px; background-color: Red;  float:left;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Green;  float:left;">
  </div>
  <div style="height: 100px; width: 100px; background-color: Yellow;  float:left;">
  </div>
</div>
```


### 浮动元素对其他元素的影响

1. 对父容器：如果父元素中的子元素都为浮动元素，而且父元素没有设置高度，那么父元素的高度会发生坍塌

2. 对其他浮动元素：如果包含块儿太窄无法容纳水平排列的全部浮动元素,那么其它浮动块儿向下移动,直到有足够的空间,如果浮动元素的高度不同,那么向下移动的时候可能被卡住

3. 对其他普通元素：普通元素无法感知浮动元素的存在，会占据原来浮动元素的位置，但会被浮动元素遮盖。

4. 对文字的影响：文字能识别到浮动元素的存在，会移动以留出空间，会出现文字围绕浮动元素的现象。下面是代码示例：

   1. 正常情况

   ```html
   <div style="border: solid 5px #0e0; width: 250px;">
     <div style="height: 50px; width: 50px; background-color: Red;"></div>
     <div style="height: 100px; width: 100px; background-color: Green;">
       11111111111
       11111111111
     </div>
   </div>
   ```

   2. 文本围绕浮动框

   ```html
   <div style="border: solid 5px #0e0; width: 250px;">
     <div style="height: 50px; width: 50px; background-color: Red; float:left;"></div>
     <div style="height: 100px; width: 100px; background-color: Green;">
       abc def ghi
       abc def ghi
       abc def ghi
     </div>
   </div>
   ```

### 清除浮动

元素的侧边不允许出现浮动元素，解决不设置高度的父容器塌陷的问题。清除浮动一般有以下几种方法：

1. 利用 clear 属性清除浮动

- 在浮动元素的最后添加一个空标签，利用 clear 属性进行清除浮动，撑开父容器。该方法的缺点是增加了一个无意义（语义）的标签，所以这种方法不可取。如：

```html
<div style="border: solid 5px #0e0; width:300px;">
      <div style="height: 100px; width: 100px; background-color: Red;  float:left;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Green;  float:left;">
      </div>
      <div style="height: 100px; width: 100px; background-color: Yellow;  float:left;">
      </div>
      <div style="clear:both;"></div>
  </div>
```

效果：

![float1](./imgs/013/float1.png)

2. 利用 BFC 清理浮动

   > BFC 的解释后文有，可以先不看这条，回过头看

利用 BFC 的第三条特性来“清浮动”，这里其实说清浮动已经不再合适，应该说包含浮动。也就是说只要**父容器**形成新的 BFC 就可以。形成新的 BFC 主要有以下方法：
- float 为 left|right
- overflow 为 hidden|auto|scroll（即非visible）
- display 为 table-cell|table-caption|inline-block
- position 为 absolute|fixed

> 使用 BFC 清除浮动会有一系列的副作用。比如：使用 float 的时候会使父容器长度缩短，而且还有个重要缺陷——父容器 float 解决了其塌陷问题，那么父容器的父容器怎么办？overflow 属性会影响滚动条和绝对定位的元素；position 会改变元素的定位方式，这是我们不希望的，display 这几种方式依然没有解决低版本IE问题。。。

3. 通用的清理浮动法案（after伪元素清除浮动 ）

```css
/*方法1*/
.clearfix{
  *zoom:1;          /*针对ie 6 7，利用hasLayout属性 */
}
.clearfix:after{
  content:"";    
  display:block;
  clear:left;
} 
/*用after在浮动元素最后添加一个伪元素，再利用clear属性清除浮动，类似方法1，不需要添加无意义的html标签*/ 

/*方法2*/
.clearfix{
  *zoom:1;
}
.clearfix:after{
  content:"";
  display:table;
  clear:both;
}
```

虽然我们得出了一种浏览器兼容的靠谱解决方案，但这并不代表我们一定得用这种方式，很多时候我们的父容器本身需要 `position：absolute` 等形成了 BFC 的时候我们可以直接利用这些属性了，要掌握原理，活学活用。总而言之清理浮动常用的两种方式：

1. 利用 clear属性，清除浮动
2. 使父容器形成BFC

## BFC

BFC 全称块级格式化上下文。[Block Format Content](http://www.w3.org/TR/CSS21/visuren.html#block-formatting)

### 特点

处在同一个 BFC 中的元素遵守下列规则：

1. 块级元素从上到下排列，内联元素从左到右排列。
2. 垂直外边距合并（相邻元素或者嵌套元素）。
3. 浮动元素与普通流中的元素重叠。
4. 一个行内元素形成了一个单独的 BFC 时，这个元素就具有了块级元素的特性，即可以设置宽高，可以设置四个方向的 margin 和 padding。

两个不同的 BFC 之间的规则：

1. BFC 会阻止垂直外边距（margin-top、margin-bottom）合并。

  - 按照 BFC 的定义，只有同属于一个 BFC 时，两个元素才有可能发生垂直 Margin 的重叠，这个包括相邻元素，嵌套元素，只要他们之间没有阻挡（例如边框，非空内容，padding 等）就会发生margin重叠。
  - 因此要解决 margin 重叠问题，只要让它们不在同一个 BFC 就行了，但是对于两个相邻元素来说，意义不大，没有必要给它们加个外壳，但是对于嵌套元素来说就很有必要了，只要把父元素设为 BFC 就可以了。这样子元素的 margin 就不会和父元素的 margin 发生重叠。

2. BFC 不会重叠浮动元素。
3. BFC 可以包含浮动，即解决浮动照成的父元素高度塌陷问题。

### 如何形成

  1. float
2. absolutely positioned elements： 
```css
  positione: absolute, fixed;
```
3. block containers (such as inline-blocks, table-cells, and table-captions) that are not block boxes,
```css
  display: inline-blocks, table-cells, table-captions;
```
4. and block boxes with 'overflow' other than 'visible' (except when that value has been propagated to the viewport) establish new block formatting contexts for their contents.

```css
  overflow: auto, hidden, scroll    
```

## 定位

CSS有三种基本的定位机制：普通流，浮动，绝对定位(absolute,fixed)

1. 普通流是默认定位方式，在普通流中元素框的位置由元素在 HTML 中的位置决定，即块级元素从上到下排列，内联元素从左到右排列。这也是我们最常见的方式。其中 position: static 与 position:relative 属于普通流的定位方式。相对定位可以看作特殊的普通流定位，元素位置是相对于它在普通流中位置发生变化
2. 浮动定位
3. 绝对定位。包括 absolute和 fixed，绝对定位的元素会呈现块级特性，哪怕是 `span` 等内联元素。

> 2 和 3 元素都会脱离文档的普通流
> 注意：position:relative 属于普通流，元素位置会发生偏移，但是并不会影响其他元素的布局

| 值       | 属性                                                         |
| -------- | ------------------------------------------------------------ |
| inherit  | 规定应该从父元素继承 position 属性的值                       |
| static   | 默认值，没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明） |
| relative | 生成相对定位的元素，相对于元素本身正常位置进行定位,因此，left:20px 会向元素的 left 位置添加 20px |
| absolute | 生成绝对定位的元素，相对于 static 定位以外的第一个祖先元素（offset parent）（padding）进行定位，如果元素没有已定位的祖先元素，那么他的位置就相对于根元素 html 来定位。元素的位置通过 left, top, right 以及 bottom 属性进行规定。不设置top等属性时，元素会贴着父元素的 padding，所以最好用时候都设置一下 |
| fixed    | 生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 left, top, right 以及 bottom 属性进行规定 |
| sticky   | CSS3 新属性，表现类似 position:relative 和 position:fixed 的合体，在目标区域在屏幕中可见时，它的行为就像 position:relative；而当页面滚动超出目标区域时，它的表现就像   position:fixed，它会固定在目标位置 |

### 绝对定位的宽度

绝对定位宽度是收缩的，包括 `position:fixed;` 和 `psoition:absolute;`。如果想撑满父容器，可以设置 width: 100%

> `绝对定位`的元素设置 `width:100%;` 实际上指的是子元素的 `width` 等于它相对于定位的那个元素的 padding+content 的宽度，而不一定是它的直接父元素的宽度。当子元素是非绝对定位的元素时 width:100% 才是指子元素的 content 等于父元素的 content 宽度。固定定位即 `position:fixed;` 的元素的宽度是受 HTML 文档即 `<html>` 元素的宽度限制。

### z-index

- 因为绝对定位的元素与普通流元素无关，所以绝对定位的元素可以覆盖页面上的其他元素，可以通过 z-index 属性控制在垂直于屏幕方向的叠放顺序，z-index 越高，元素位置越靠上。
- z-index 规定了元素在Z轴（距离用户远近）上的顺序，值越大离用户越近、越在上层。
- z-index 仅在设置了不在普通流中的元素生效（适用于浮动元素），且 z-index 的值只能在兄弟元素之间比较。
- z-index 默认值为 auto, 不建立层叠上下文。设置为 0 则会建立层叠上下文。

关于 z-index 更详细的内容请参考 [张鑫旭博客](http://www.zhangxinxu.com/wordpress/?p=5115)

### position:relative 和负 margin

- posotion: relative 只相对于自己原本位置发生偏移，不影响其他普通流中元素的位置。
- 负 margin 除了让元素自身发生偏移还会影响其他普通流中的元素

## 垂直外边距合并

外边距合并的三个场景：

1. 同一个 BFC 中，且同属于普通流中的垂直相邻元素外边距合并。
2. 父子元素间没有阻挡（如：边框、非空内容、padding 等）时发生外边距合并
3. 空元素外边距合并。这个基本不用去管，比如以下例子：

```html
<style>
  #d1 {
    margin-top:50px;
    margin-bottom:20px;
  }
</style>
// 本来应该是上 margin 50px，下 margin 20px，但是最终会合并为一个 margin，50px
<div id="d1">
</div>
```

合并规则：

1. margin 都是正值的时候，取两者之间的较大值。
2. margin 都是负值时，取绝对值较大的值。
3. margin 有正值有负值的时候，先取出负 margin 中绝对值较大的，然后和正 margin 最大值相加。
4. 所有毗邻的 margin 一起参与运算，不能分布进行。

不让相邻元素外边距合并的方法：

1. 不在一个 BFC 中。  
3. margin 在垂直方向上不相邻，即中间有一个非空元素，或者空元素有 padding 或 margin。

[父子外边距合并](http://js.jirengu.com/mixit/1/edit)

不让父子元素外边距合并的方法：

1. 子元素和父元素的兄弟元素之间被非空内容如 padding、border 分隔开，即为父元素添加非空内容、padding、border。
2. 父元素形成一个新的 BFC

参考：

- [张鑫旭博客](http://www.zhangxinxu.com/wordpress/?p=5115)