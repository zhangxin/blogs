# Ajax

## jQuery.ajax( [settings ] )

先看个例子

```javascript
$.ajax({
    url: 'xxx.php',
    method: 'GET',
    data: {
        name: 'Byron',
        age: 24,
        sex: 'Male'
    },
    dataType: dataType  // dataType：从服务器返回的预期的数据类型。默认：智能猜测（xml, json, script, 或 html）
}).done(function(result){
    console.log(result);
}).fail(function(jqXHR, textStatus){
   consloe.log(textStatus);
});
```

这样我们就发送了一个 get 请求

方法提供了几个常用的 setting

1. async：默认设置下，所有请求均为异步请求（也就是说这是默认设置为 true ）。如果需要发送同步请求，请将此选项设置为 false
2. beforeSend：请求发送前的回调函数，用来修改请求发送前 jqXHR 对象，此功能用来设置自定义 HTTP 头信息，等等。该 jqXHR 和设置对象作为参数传递
3. cache：如果设置为 false ，浏览器将不缓存此页面。注意: 设置 cache 为 false 将在 HEAD 和 GET 请求中正常工作。它的工作原理是在 GET 求参数中附加 "_={timestamp}"
4. context：这个对象用于设置 Ajax 相关回调函数的上下文。 默认情况下，这个上下文是一个 ajax 请求使用的参数设置对象
5. data：发送到服务器的数据。将自动转换为请求字符串格式。GET 请求中将附加在 URL 后面，POST 请求作为表单数据
6. headers：一个额外的`{键:值}`对映射到请求一起发送。此设置会在 beforeSend 函数调用之前被设置；因此，请求头中的设置值，会被 beforeSend 函数内的设置覆盖
7. method：HTTP 请求方法 (比如："POST", "GET ", "PUT"，1.9 之前使用 “type”)

了解了这些参数，使用 jQuery 处理 ajax 请求就简单了

```javascript
$.ajax({
  method: "POST",
  url: "some.php",
  data: { name: "John", location: "Boston" }
}).done(function( msg ) {
  alert( "Data Saved: " + msg );
});
```

除了这个方法，jQuery 还提供了一些额外的方法

## jQuery.get( [settings] ) / jQuery.post( [settings ] )

这两个方法专门用来处理`get`和`post`请求

```javascript
$.get("test.cgi", { name: "John", time: "2pm" },
   function(data){
     alert("Data Loaded: " + data);
   });
$.post('ajax/test.html', function(data) {
  $('.result').html(data);
});
```

## jQuery.getJSON( url [, data ] [, success(data, textStatus, jqXHR) ] )

使用一个 HTTP GET 请求从服务器加载 JSON 格式的数据，这是一个 Ajax 函数的缩写，这相当于:

```javascript
$.ajax({
  dataType: "json",
  url: url,
  data: data,
  success: success
});
```

## .load( url [, data ] [, complete(responseText, textStatus, XMLHttpRequest) ] )

从服务器载入数据并且将返回的 HTML 代码并插入至 匹配的元素中。等于说做了一些 DOM 相关的操作，基本不用。

```javascript
$('#result').load('ajax/test.html')
```

## .serialize() / serializeArray()

将用作提交的表单元素的值编译成字符串，方法没有参数，使用标准的 URL-encoded 符号上建立一个文本字符串. 它可以对一个代表一组表单元素的 jQuery 对象进行操作，比如`<input>`, `<textarea>`, 和 `<select>`:

```javascript
<form id="holder">
  <input type="text" name="a" value="1"/>
  <div>
    <input type="text" name="b" value="2" id="b" />
  </div>
  <input type="hidden" name="c" value="3" id="c" />
  <div>
    <input type="checkbox" name="f" value="8" checked="true"/>
    <input type="checkbox" name="f" value="9" checked="true"/>
  </div>
</form>

$("#holder").serialize(); //a=1&b=2&c=3&f=8&f=9

$("#holder").serializeArray();
/*
    [
      {name: 'a', value: '1'},
      {name: 'b', value: '2'},
      {name: 'c', value: '3'},
      {name: 'f', value: '8'},
      {name: 'f', value: '9'}
    ]
*/
```

serialize 和 serializeArray 都是针对 JQuery 对象（选中的 FORM 元素）进行操作，只是返回值格式不同而已。这里特别要注意：这 2 个 API 只能操作 form，如果将 holder 改成 div，会发现不起作用。

# jQuery 的一些常用方法

## .each( function(index, Element) )

遍历一个 jQuery 对象，为每个匹配元素执行一个函数

```javascript
$( "li" ).each(function( index ) {
  console.log( index + ":" + $(this).text() ); // this代表当前元素，是一个 DOM 元素
});
```

## jQuery.each( collection, callback(indexInArray, valueOfElement) )

一个通用的迭代函数，它可以用来无缝迭代对象和数组。数组和类似数组的对象通过一个长度属性（如一个函数的参数对象）来迭代数字索引，从 0 到 length - 1。其他对象通过其属性名进行迭代。

```javascript
var obj = {
  "flammable": "inflammable",
  "duh": "no duh"
};
$.each( obj, function( key, value ) {
  alert( key + ": " + value );
});
```

## .map( callback(index, domElement) )

通过一个函数匹配当前集合中的每个元素，产生一个包含新的 jQuery 对象

```javascript
$('div').map(function(i, ele){
    return this.id;
});
```

## jQuery.extend([deep,] target [, object1 ] [, objectN ] )

1. 当我们提供两个或多个对象给`$.extend()`，对象的所有属性都添加到目标对象（target参数）。
2. 如果只有一个参数提供给`$.extend()`，这意味着目标参数被省略。在这种情况下，jQuery对象本身被默认为目标对象。这样，我们可以在 jQuery 的命名空间下添加新的功能。这对于插件开发者希望向 jQuery 中添加新函数时是很有用的

目标对象（第一个参数）将被修改，并且将通过 $.extend() 返回。然而，如果我们想保留原对象，我们可以通过传递一个空对象作为目标对象：

```javascript
var object = $.extend({}, object1, object2);
```

在默认情况下，通过`$.extend()`合并操作不是递归的;

如果第一个对象的属性本身是一个对象或数组，那么它将完全用第二个对象相同的key重写一个属性。这些值不会被合并。如果将 `true`作为该函数的第一个参数，那么会在对象上进行递归的合并。

```javascript
var object1 = {
  apple: 0,
  banana: { weight: 52, price: 100 },
  cherry: 97
};
var object2 = {
  banana: { price: 200 },
  durian: 100
};

// Merge object2 into object1
$.extend( object1, object2 );
```

## .clone( [withDataAndEvents ] )

.clone()方法深度复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点

通常我们将页面上一个元素插入到DOM里另一个地方，它会被从老地方移走，类似剪切的效果

```javascript
$('.hello').appendTo('.goodbye');

<div class="container">
  <div class="goodbye">
    Goodbye
    <div class="hello">Hello</div>
  </div>
</div>
```

但是我们如果需要的是复制而不是剪切，我们可以像下面这样写代码：

```javascript
$('.hello').clone().appendTo('.goodbye');
```

## .index() / .index(selector)/ .index(element)

从给定集合中查找特定元素 index

1. 没参数返回第一个元素 index
2. 如果参数是 DOM 对象或者 jQuery 对象，则返回参数在集合中的 index
3. 如果参数是选择器，返回第一个匹配元素 index，没有找到返回 -1

看个例子

```javascript
var listItem = $( "#bar" );
alert( "Index: " + $( "li" ).index( listItem ) );
```

## .ready( handler )

当 DOM 准备就绪时，指定一个函数来执行。

虽然 JavaScript 提供了 load 事件，当页面呈现时用来执行这个事件，直到所有的东西，如图像已被完全接收前，此事件不会被触发。

在大多数情况下，只要 DOM 结构已完全加载时，脚本就可以运行。传递处理函数给 `.ready()` 方法，能保证 DOM 准备好后就执行这个函数，因此，这里是进行所有其它事件绑定及运行其它 jQuery 代码的最佳地方。

如果执行的代码需要在元素被加载之后才能使用时，（例如，取得图片的大小需要在图片被加载完后才能知道），就需要将这样的代码放到 load 事件中。

下面两种语法全部是等价的：

- $(document).ready(handler)
- $(handler)

我们经常这么使用