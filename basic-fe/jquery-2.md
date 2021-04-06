# jQuery 动画&Ajax&常用方法

## 基础

### .hide([duration ] [,easing ] [,complete ])

用于隐藏元素，没有参数的时候等同于直接设置 `display` 属性

看几个例子

```javascript
 $('.target').hide();  //等同于 $('.target').css('display', 'none')
```

```javascript
}) $('#book').hide(300, function() {
alert('Animation complete.');})
```

```javascript
  $('#book').hide(300, 'linear', function() {
    alert('Animation complete.');
  })
```

### .show( [duration ] [, easing ] [, complete ] )

用于显示元素，用法和 `hide` 类似

### .toggle( [duration ] [, easing ] [, complete ] )

> 事件处理套件也有一个名为.toggle()方法。哪一个被调用取决于传递的参数的设置

用来切换元素的隐藏、显示，类似于 `toggleClass`，用法和 `show`、`hide` 类似。因为 jQuery 能记住元素原来的 CSS 属性，比如 display 等。

## 渐变

### .fadeIn( [duration ] [, easing ] [, complete ] )

通过淡入的方式显示匹配元素，参数含义和上面相同

```javascript
$('#book').fadeIn('slow', function() {
// Animation complete
});
```

### .fadeOut( [duration ] [, easing ] [, complete ] )

通过淡出的方式隐藏匹配元素

```javascript
$('#book').fadeOut('slow', function() {
// Animation complete.
});
```

### .fadeTo( duration, opacity [, easing ] [, complete ] )

通过匹配的元素的不透明度动画，来显示或隐藏它们，方法执行匹配元素的不透明度动画。当被可见元素调用时，元素不透明度一旦达到 0，display 样式属性设置为 none ，所以元素不再影响页面的布局。

```javascript
$('#book').fadeTo('slow', 0.5, function() {
  // Animation complete.
});
```

### .fadeToggle( [duration ] [, easing ] [, complete ] )

调整匹配元素的透明度，方法通过匹配元素的不透明度做动画效果

```javascript
$("button:first").click(function() {
  $("p:first").fadeToggle("slow", "linear");
});
```

## 滑动

### .slideDown( [duration ] [, easing ] [, complete ] )

用滑动动画显示一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面的下面部分滑下去，弥补了显示的方式

```
$('#book').slideDown('slow', function() {
    // Animation complete.
});
```

### .slideUp( [duration ] [, easing ] [, complete ] )

用滑动动画隐藏一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面的下面部分滑上去，当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局。 display 样式属性将被设置为none，以确保该元素不再影响页面布局。

```
$('#book').slideUp('slow', function() {
    // Animation complete.
});
```

### .slideToggle( [duration ] [, easing ] [, complete ] )

用滑动动画显示或隐藏一个匹配元素，方法将给匹配元素的高度的动画，这会导致页面中，在这个元素下面的内容往下或往上滑。display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值。

如果一个元素的display属性值为inline，然后是隐藏和显示，这个元素将再次显示inline。当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局。

```javascript
$('#clickme').click(function() {
 $('#book').slideToggle('slow', function() {
 // Animation complete.
 });
});
```

## 动画队列

```javascript
$box.hide(1000, function(){
   $box.show(1000, function(){
     $box.fadeOut('slow',function(){
       $box.fadeIn('slow',function(){
         $box.slideUp(function(){
           $box.slideDown(function(){
             console.log('动画执行完毕')
           })
         })
       })
     })
   })
})
//等价于
$box.hide(1000)
    .show(1000)
    .fadeOut()
    .fadeIn()
    .slideUp()
    .slideDown(function(){
      console.log('真的完毕了')
    })
```

## 自定义动画

上面几个简单的动画不能满足需求的时候，jQuery 提供了自定义动画行为的方法

动画本质还是操作 CSS，只是让状态变化有个过渡，所以 CSS 还是要写对。动画可以链式调用，如果动画很复杂，定义出关键帧即可。关键帧就是动画队列，使用动画时候心里要有动画队列的概念。

可以定义一个成员是 CSS 对象的数组，每个数组代表一个状态，遍历数组将成员传递给 `.animate`。

### .animate( properties [, duration ] [, easing ] [, complete ] )

[官方文档](https://api.jquery.com/animate/)

properties是一个 CSS 属性和值的对象，动画将根据这组对象移动。

所有用于动画的属性必须是数字的。例如，`width`, `height`或者`left`可以执行动画，但是`background-color`不能，除非使用[jQuery.Color()](https://github.com/jquery/jquery-color)插件。

CSS简写属性（例如font, background, border）没有得到充分的支持。

除了定义数值，每个属性能使用`'show'`, `'hide'`, 和 `'toggle'`。这些快捷方式允许定制隐藏和显示动画用来控制元素的显示或隐藏。

动画属性也可以是一个相对值。如果提供一个以 `+=` 或 `-=` 开始的值，那么目标值就是以这个属性的当前值加上或者减去给定的数字来计算的。

`fontSize`的或相当于CSS的 `'font-size'` ，而不是简单的`'font'`。这跟 JS 的 DOM api 特性符合。

```javascript
$('#clickme').click(function() {
  $('#book').animate({
    opacity: 0.25,
    left: '+=50',
    height: 'toggle'
  }, 5000, function() {
    // Animation complete.
  });
});
```

### .clearQueue()

清除动画队列中未执行的动画

### .finish

停止当前动画，并清除动画队列中所有未完成的动画，最终展示动画队列最后一帧的最终状态

### .stop( [queue ] [, clearQueue ] [, jumpToEnd ] )

停止当前正在运行的动画。比较复杂具体看文档。

- **queue**

  停止动画队列的名称。

- **clearQueue**

  一个布尔值，指示是否取消所有动画队列。默认 `false`，即执行一次 `.stop()` 只取消一个动画队列。值为 `true` 时取消后续所有动画。

- **jumpToEnd**

  一个布尔值指示是否当前动画立即完成。默认`false`。