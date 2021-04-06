# jQuery

## 前端不可能不知道 jQuery

据统计，全世界排名前 100 的网站，有 46% 使用 jQuery 2006 年 8 月26 日最初版本，只是提供了一个友好的 $('选择器')

## 为什么要用 jQuery

DOM API

- 难用
- 存在兼容性问题
- 功能太少，不能与时俱进

jQuery

- 兼容性好
- API 友好
- 功能强大，与时俱进

## 什么时候适合用 jQuery

- DOM 操作较多（事件监听）
- 简单的 AJAX
- 需要兼容多款浏览器

## 什么时候不用 jQuery

- 页面交互极为简单
- 页面对流量有苛刻的要求
- 上级强制、团队已经有了 jQuery 的代替品

## jQuery 做什么

- 选择网页元素
- 改变结果集
- 元素的操作：取值和赋值
- 元素的操作：移动
- 元素的操作：复制、删除和创建
- 工具方法
- 事件操作
- 特殊效果
- AJAX
- http://devdocs.io/jquery/

## jQuery版本问题

- 1.x 与 2.x 主要是兼容范围不同

## jQuery 的两种 API

jQuery 有且只有如下两种 API ，即 `$.xxx()` 和 `$(选择器).xxx()`

jQuery 的链式调用是 jQuery 的特色，因为 jQuery 对象执行任何函数的返回值都还是原来的 jquery 对象。

```
$.noConflict()
$.each()
$('ul').addClass()
$('p').text('hi')
```

## ready

$(handler)    

 页面上的所有 DOM 元素加载完成之后再去执行 handler 函数，相当于原生 JS 的 DOMContentLoaded 事件。比 window.load 事件时机更早，后者是页面所有元素加载完成，包括图片 CSS 等

```javascript
$(callback)
window.onload 事件
document 的 DOMContentLoaded 事件
$( document ).ready( handler )
$().ready( handler ) (this is not recommended)
$( handler )
```

## 使用jQuery获取元素

### 选择器

我们可以通过 `document.getElementById` 等方法获取 DOM 对象，但是方法名称长，使用不方便，而且功能有限，不能像 CSS 选择器那样灵活。

jQuery 定义了一套选择器规则，和 CSS 选择器目的一样，都是为了选择出符合特定规则的元素。讲 jQuery 不得不提到其选择器，这是 jQuery 能够快速流行的非常重要的原因，为了方便使用者 jQuery 刻意和 CSS 选择器使用相同的语法，几乎支持所有类型的 CSS3 选择器，当然也有一些其特定的选择器。

学会了 CSS 选择器基本等同于学会了 jQuery 选择器。

### 与获取元素相关的常用方法

#### 根据下标筛选元素

| 方法名        | 含义及示例                                                   |
| :------------ | ------------------------------------------------------------ |
| .eq(index)    | `$('div').eq(3)`  //  获取结果集中的第 3 个 jQuery 对象      |
| .get([index]) | `$('div').get(3)`  //  获取结果集中的第 3个 DOM 对象。与 `[]` 法获取结果一样 |

我们可以通过类数组下标的获取方式或者 get 方法获取指定 index 的 DOM 对象，也就是我们说的 jQuery 对象转 DOM 对象。`get()`不写参数把所有 jQuery 对象转为 DOM 对象返回。

注意 jQuery 元素（对象）和 DOM元素（对象）的区别

前者是对 DOM 元素进行了一些封装得到的对象，和原生 DOM 不是一样的东西。`$('xxx')` 选中的是 jQuery 元素，`document.qureyselector('xxx')` 选中的是原生 DOM 元素。原生 DOM 对象只能使用原生 js 的 api。jQuery 元素使用 jQuery 的 api。二者可以相互转化。

#### 兄弟元素获取

| 方法名                                     | 含义及示例                                                   |
| ------------------------------------------ | ------------------------------------------------------------ |
| .next([selector]), .prev([selector])       | `next` 取得匹配的元素集合中每一个元素紧邻的后一个同辈元素的元素集合。如果提供一个选择器，那么只有紧跟着的兄弟元素满足选择器时，才会返回此元素。`prev`正好相反，获取元素之前的同辈元素 。`.$('.test').next(); $('.test').prev('li');` |
| .nextAll([selector]), .prevAll([selector]) | `nextAll` 获得匹配元素集合中每个元素所有后面的同辈元素，选择性筛选的选择器，`prevAll` 与之相反，获取元素前面的所有同辈元素。同样可以提供一个选择器 |
| .siblings([selectors])                     | 获得匹配元素集合中每个元素的所有兄弟元素，可以提供一个可选的选择器 `$('li.third-item').siblings()` |

#### 父子元素获取

| 方法名                | 含义及示例                                                   |
| --------------------- | ------------------------------------------------------------ |
| .parent([selector])   | 取得匹配元素集合中，每个元素的父元素，可以提供一个可选的选择器 `$('li.item-a').parent()` |
| .parents([selector])  | 获得集合中每个匹配元素的祖先元素，可以提供一个可选的选择器作为参数 `$('li.item-a').parents('div')` |
| .children([selector]) | 获得匹配元素集合中每个元素的直接子元素，选择器选择性筛选 `$('ul.level-2').children()` |
| .find([selector])     | 查找符合选择器的后代元素 `$('ul').find('li.current')`        |

#### 筛选当前结果集

| 方法名                                            | 含义及示例                                                   |
| ------------------------------------------------- | ------------------------------------------------------------ |
| .first()                                          | 获取当前结果集中的第一个对象                                 |
| .last()                                           | 获取当前结果集的最后一个对象                                 |
| .filter(selector), .filter(function(index))       | 筛选当前结果集中符合条件的对象，参数可以是一个选择器或者一个函数  `$('li').filter(':even')  $('li').filter(function(index) {return index % 3 == 2; }`) |
| .not(selector), .not(function(index))             | 从匹配的元素集合中移除指定的元素，和 filter 相反             |
| .is(selector), is(function(index)), is(dom/jqObj) | 判断当前匹配的元素集合中的元素，是否为一个选择器，DOM 元素，或者 jQuery 对象，如果这些元素至少一个匹配给定的参数，那么返回 true。  `if ( $target.is("li") ) {$target.css("background-color", "red");}` |
| .has(selector), .has(dom)                         | 筛选匹配元素集合中的那些有相匹配的选择器或 DOM 元素的后代元素 `$('li').has('span')` |

最下面两行用的不多。

## jQuery DOM操作

使用 jQuery 修改 DOM 相当简单

### 创建元素

只需要把 DOM 字符串传入`$`方法即可返回一个 jQuery 对象

```javascript
var obj = $('<div class="test"><p><span>Done</span></p></div>');
```

### 添加元素

#### .append(content[,content]) / .append(function(index,html))

给一个元素头部（内部最前）插入一个元素

1. 可以一次添加多个内容，内容可以是 `DOM对象`、`HTML string`、 `jQuery对象`。参数 (content[,content]) 中的 [,content] 表示可选择一次插入多个元素。
2. 如果参数是 `function`，function 可以返回 DOM 对象、HTML string、 jQuery 对象，参数是集合中的元素位置与原来的 HTML 值。

看几个例子

```javascript
$( ".inner" ).append( "<p>Test</p>" );
$( "body" ).append( $newdiv1, [ newdiv2, existingdiv1 ] );
$( "p" ).append( "<strong>Hello</strong>" );
$( "p" ).append( $( "strong" ) );
$( "p" ).append( document.createTextNode( "Hello" ) );
```

下面这些方法使用跟 append 类似，记住名字就相当于记住了如何使用。总共 4 对 8 个方法

1. `.append(content[,content]) / .append(function(index,html))`

2. `.appendTo(target)`

3. `.prepend(content[,content]) / .prepend(function(index,html))`

4. `.prependTo(target)`

5. `.before(\[content\][,content]) / .before(function)`

在对象前面（不是头部，而是外面，和对象并列同级）插入内容，参数和 append 类似

6. `.insertBefore(target)`

7. `.after([content][,content]) / .after(function(index))`

8. `.insertAfter(target)`

### 删除元素

#### .remove([selector])

删除被选元素（及其子元素）

```javascript
 $("#div1").remove();
```

我们也可以添加一个可选的选择器参数来过滤匹配的元素

```javascript
$('div').remove('.test');
```

#### .empty()

清空被选择元素内所有子元素

```javascript
$('body').empty();
```

#### .detach()

`.detach()` 方法和 `.remove()`一样, 除了 `.detach()` 保存所有 jQuery 数据和被移走的元素相关联。当需要移走一个元素，不久又将该元素插入 DOM 时，这种方法很有用。

### 包裹元素

#### wrap(wrappingElement) / .wrap(function(index))

为每个对象包裹一层 HTML 结构，可以是 selector, element, HTML string, jQuery object

```javascript
<div class="container">
  <div class="inner">Hello</div>
  <div class="inner">Goodbye</div>
</div>
```

包裹元素

```
$( ".inner" ).wrap( "<div class='new'></div>" );
```

看看结果

```
<div class="container">
  <div class="new">
    <div class="inner">Hello</div>
  </div>
  <div class="new">
    <div class="inner">Goodbye</div>
  </div>
</div>
```

#### .wrapAll(wrappingElement)

把所有匹配对象包裹在同一个 HTML 结构中

```html
<div class="container">
  <div class="inner">Hello</div>
  <div class="inner">Goodbye</div>
</div>
```

包裹元素

```javascript
$(".inner").wrapAll( "<div class='new' />");
```

看看结果

```html
    <div class="container">
      <div class="new">
        <div class="inner">Hello</div>
        <div class="inner">Goodbye</div>
      </div>
    </div>
```

#### .wrapInner(wrappingElement) / .wrapInner(function(index))

包裹匹配元素内容，这个不好描述，一看例子就懂

```htnl
<div class="container">
  <div class="inner">Hello</div>
  <div class="inner">Goodbye</div>
</div>
```

包裹元素

```javascript
$( ".inner" ).wrapInner( "<div class='new'></div>");
```

执行结果

```html
<div class="container">
  <div class="inner">
    <div class="new">Hello</div>
  </div>
  <div class="inner">
    <div class="new">Goodbye</div>
  </div>
</div>
```

#### .unwrap()

把 DOM 元素的 parent 移除

```javascript
pTags = $( "p" ).unwrap();
```

### HTML 操作

#### html([string])

这是一个读写两用的方法，用于获取/修改元素的 innerHTML。jQuery 方法有一个特点，就是参数为空的时候是获取，有参数的时候是设置

1. 当没有传递参数的时候，返回元素的 innerHTML
2. 当传递了一个 string 参数的时候，修改元素的 innerHTML 为参数值

看个例子

```javascript
$('div').html()
$('div').html('123')
```

后续这种读写两用的方法很多，原理都类似

#### text()

和 `html()` 方法类似，操作的是 DOM 的 innerText 值

## 属性&CSS操作

### 属性相关

#### .val([value])

读写双用的方法，用来处理 input 的 value

#### .attr(attributeName)

获取元素特定属性的值

```javascript
var title = $( "em" ).attr( "title" );
```

#### .attr(attributeName,value) / .attr(attributesJson) / .attr( attributeName, function(index, attr) )

为元素属性赋值

```javascript
$( "#greatphoto" ).attr( "alt", "Beijing Brush Seller" );

$( "#greatphoto" ).attr({
  alt: "Beijing Brush Seller",
  title: "photo by Kelly Clark"
});

$( "#greatphoto" ).attr( "title", function( i, val ) {
  return val + " - photo by Kelly Clark";
});
```

#### .removeAttr()

为匹配的元素集合中的每个元素中移除一个属性（attribute）

```javascript
$('div').removeAttr('id');
```

#### .prop()/.removeProp()

这两个方法是用来操作元素的`property`的，property 和 attibute 是非常相似的概念，可以看看 [jQuery的attr与prop](http://www.cnblogs.com/dolphinX/p/3348582.html)

### CSS相关

`.css()` 和`attr()`非常相似，用来处理元素的 CSS。jQuery 的 `.css()` 方法获取的是计算后的样式

#### .css(propertyName) / .css(propertyNames)

获取元素 style 特定 property 的值

```javascript
var color = $( this ).css( "background-color" );

var styleProps = $( this ).css([
  "width",
  "height",
  "color",
  "background-color"
]);
```

#### .css(propertyName,value) / .css( propertyName, function(index, value) ) / .css( propertiesJson )

设置元素 style 特定 property 的值

```js
$( "div.example" ).css( "width", function( index ) {
  return index * 50;
});

$( this ).css( "width", "+=200" );

$( this ).css( "background-color", "yellow" );

$( this ).css({
  "background-color": "yellow",
  "font-weight": "bolder"
});
```

### class 操作

#### .addClass(className) / .addClass(function(index,currentClass))

为元素添加 class，不是覆盖原 class，是追加，也不会检查重复

#### .removeClass([className]) / ,removeClass(function(index,class))

移除元素单个/多个/所有class

#### .hasClass(className)

检查元素是否包含某个class，返回true/false

```javascript
$( "#mydiv" ).hasClass( "foo" )
```

#### .toggleClass(className)

toggle 是切换的意思，方法用于切换，switch是个 bool 类型值，这个看例子就明白

```javascript
<div class="tumble">Some text.</div>
```

第一次执行

```javascript
$( "div.tumble" ).toggleClass( "bounce" )

<div class="tumble bounce">Some text.</div>
```

第二次执行

```javascript
$( "div.tumble" ).toggleClass( "bounce" )

<div class="tumble">Some text.</div>
```

## 事件

事件处理中最头疼的就是浏览器兼容问题，jQuery 封装了很好的 API，可以方便的进行事件处理

在 1.7 之前的版本中 jQuery 处理事件有多个方法， (google 搜索: jquery live bind degelate)作用各不相同，后来统一的使用 `on`/`off` 方法

### .on( events [,selector ] [,data ], handler(eventObject) )

看起来参数及其复杂，我们看一下各个参数的意思

1. events：一个或多个空格分隔的事件类型和可选的命名空间，或仅仅是命名空间，比如"click", "keydown.myPlugin", 或者 ".myPlugin"
2. selector：一个选择器字符串，用于过滤出被选中的元素中能触发事件的后代元素，通常在事件代理时候使用。如果选择器是 null 或者忽略了该选择器，那么被选中的元素总是能触发事件
3. data：当一个事件被触发时，要传递给事件处理函数的 event.data
4. handler(eventObject)：事件被触发时，执行的函数。若该函数只是要执行 return false 的话，那么该参数位置可以直接简写成 false

看几个例子

```javascript
<div class="box">
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
  </ul>
</div>
<input id="ipt" type="text"> <button id="btn">添加</button>
<div id="wrap">
</div>

<script>
$('.box li').on('click', function(){
    console.log(1)
  var str = $(this).text()
  $('#wrap').text(str)
})

//等同于。因为 jQuery 还提供了一些常见事件的快捷方式，具体有哪些去谷歌搜索
$('.box>ul>li').click(function(){
    console.log(2)
  var str = $(this).text()
  $('#wrap').text(str)
})

//也可以这样写
$('.box li').on('click.hello', function(){
    console.log(3)
  var str = $(this).text()
  $('#wrap').text(str)
})
//命名空间没什么特别的作用，只不过在解绑事件时便于区分绑定的事件
$('.box li').off('click.hello')

//可是用如下方法新增的元素是没绑定事件的
$('#btn').on('click', function(){
  var value = $('#ipt').val()
  $('.box>ul').append('<li>'+value+'</li>')
})

//我们可以用事件代理
$('.box ul').on('click', 'li', function(){
  var str = $(this).text()
  $('#wrap').text(str)
})

//上面代码相当于原生 js 的
document.querySelector('.box ul').addEventListener('click', function(e){
    if(e.target.tagName.toLowerCase() === 'li'){  // e.target 是原生 dom 对象


        //do something
    }
})

//绑定事件的时候我们也可以给事件附带些数据，只不过这种用法很少见
$('.box').on('click', {name: 'hunger'}, function(e){
    console.log(e.data)
})
```

### .one( events [, selector ] [, data ], handler(eventObject) )

同 on，绑定事件，但只执行一次

### .off( events [, selector ] [, handler ] )

移除一个事件处理函数

```javascript
$('.box li').off('click')
```

### .trigger( eventType [, extraParameters ] )

根据绑定到匹配元素的给定的事件类型执行所有的处理程序和行为。即用 JS 模拟用户操作

```javascript
$('#foo').on('click', function() {
  console.log($(this).text())
});
$('#foo').trigger('click')
```

想在一个窗口显示一个内容，除了使用背景外还可以让父容器宽高固定然后子容器宽高等于父容器 然后设置 overflow: hidden

## 调试技巧

不知道 this 代表什么可以使用 console.log 打印出来看看。

几个疑问，留给自己慢慢思考

1. jQuery 是怎么处理多个参数的
2. jQuery 是怎么把事件传给回调函数的
3. jQuery .on 的 this
4. 使用 argument[0] 测试 .on 的参数
