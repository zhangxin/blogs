# let&const

ES6 在 2015 年出现，现在已经是前端的事实标准。已经得到广泛的支持。

学习顺序：ES5 ---> ES6。因为 ES6 包含了 ES5

ES 6 新特性一览：[新特性](https://frankfang.github.io/es-6-tutorials/)

ES5 ---> ES6 就是一部 JS 打脸史，很多旧的东西被推翻，很多以前抛弃的新特性被加入。即使 JS 有这样那样的问题，但是生命力非常顽强，全世界开发者都喜欢用。

## ES 6 如何学

1. 快速通览，然后使用
2. 边使用边加深印象

## 自学的问题

当不知道一个语法为什么要存在

1. 触类旁通，去看看其他语言有没有这个语法，怎么用的
    - 比如 symbol，以前 JS 没有 symbol 这种类型。ES6 新加入了 symbol，很多前端知道这种语法，但是很少使用，原因就是不知道何时用，怎么用。这种情况下可以参考其他语言，比如 Ruby 等，看看它们是怎么使用的。
3. 反证法，如果不用这个语法，该怎么实现需求

## 为什么会有 let

首先先了解下目前存在的变量声明的方式（普通变量声明，不包括函数声明）

```javascript
a = 1
var a = 1
// 上面两个是 ES3 的语法，下面是 ES6 语法
let a = 1
const a = 1
```

JS 为什么要给变量声明这么简单的语法都做一下改变呢？很明显是 var 不够好用，会给开发者带来这样那样的问题或者使用起来不方便。

首先来看：

```javascript
a = 1
```

一般认为上面的语句声明了一个全局变量 a，但是事实却不一定是这样。直接声明 `a = 1` 确实声明了一个全局变量，但是也有例外。比如下面的代码

```javascript
function fn() {
  var a
  function fn2() {
    a = 1
  }
}
```

上面的代码，`a = 1` 就没有声明全局变量。也就是说，只有在没有变量局部 a 的时候，`a = 1` 才会隐式的声明一个全局变量，当已经有局部变量 a 的情况下，`a = 1` 只是一个简单的赋值操作。所以说 `a = 1` 语义不明，不要使用。

下面看 `var a = 1`。这样声明变量的一个问题是，不管在哪里声明的变量，都会被提升到当前作用域的头部，会出现很多不合逻辑的结果，比如下面：

```javascript
function fn() {
  if(true) {
    console.log(a)  // 1
  } else {
    // 这里不会执行
    var a = 1
    console.log(2) //2
  }
}

fn()
```

在上面的代码中，else 代码块中的代码实际上是不会执行的。但是如果把 `var a = 1` 删除，那么 `1` 就会报错。这就是因为变量提升了。一行不会执行的代码，影响了会执行的代码的结果，这是不合逻辑的，令很多人头痛。

还有一个问题是，全局变量是不应该被使用的，很容易被修改导致出错。但是用 var 声明出一个非全局变量是非常麻烦的，因为 var 声明的变量没有其他语言几乎都有的块作用域。

```javascript
{
  var a = 1
}

console.log(a)  // 1
```

ES 5 只有函数作用域，因此想构造出一个局部变量，就得按照下面做

```javascript
// 第一步
function fn() {
 var a = 1  // a 是一个局部变量，但是又多了一个全局变量 fn。等于全局变量数目没变
}

// 我们的本意是消灭全局变量，但是隐藏了 a 又多了 fn。为了解决上面的问题，就要声明一个立即执行函数
(function fn() {
  var a = 1
}())
```

为了构造一个局部变量都要做这么多工作，非常不方便，因此 let 应运而生。let 的出现就是为了解决局部变量的问题。

```javascript
{
  let a = 1
}

console.log(a)  // 报错
```

let 是一个很简便的方法使用局部变量，但在 ES6 之前，却要用立即执行函数这种臃肿的语法，给新人带来了很多困扰。

## let 的几个特点

1. let 声明的变量的作用域在最近的 {..} 之间
2. 在一个块作用域中，在用 let 声明变量的语句执行完之前，是不能使用变量的，使用就报错，也就是说必须先声明再使用，这就减少了很多歧义。let                                       语句到当前作用域顶部的区域，叫做临时死区（Temp Dead Zone）。在临时死区中不能使用 let 声明的变量。

```javascript
{
  let a = 1
  {
    console.log(a)  // 会报错，即使父作用域中声明了 a。但是本作用域中如果再次声明的话，依然会有 TDM
    let a = 1
    {
      let a = 1
      {
        console.log(a) // 本作用域没有再次声明 a,直接用父作用域的，反而不会报错
      }
    }
  }
}
```

3. 在同一个块作用域下，不能重复声明变量

```javascript
{
  let a = 1
  let a = 1  // 报错
}
```

## const

const 除了具有上面 3 个特点外，还有以下特点

const 用来声明一个变量，有且只有一次赋值机会，并且在声明时候就应该马上赋值。

```javascript
const PI = 3.1415926
PI = 3.1415926   // 报错，不能重复赋值
const A // 报错，不能只声明不赋值
```

抛弃 var 吧，拥抱更好的 let。

## 面试题

```javascript
for(var i = 0; i < 6; i ++) {
  function fn() {
    console.log(1)
  }

  fn()  // code1

  button.onclick = fn // code2
}

console.log(1)  // code3  输出 6
```

首先只看 code1，很明显，code1 的输出是 1 到 6，因为每次循环时候，不等 i 变化 fn 函数就执行了。code 2 代表给一个 button 上绑定 fn，点击按钮时候 fn 执行，code2 的结果明显点击时候输出 6。因为这段代码从头到尾只有一个 i，code3 的输出是 6，用户的手速再快也比不上代码的执行速度快，点击 button 之前 code3 已经执行完了，i 已经变成 6 了，code2 只能输出 6。要注意代码执行的时机。

```javascript
var liTags = document.querySelectorAll('li')

for (var i = 0; i < liTags.length; i++) {  // liTags.length = 6
  liTags[i].onclick = function() {
    console.log(i)
  }
}
console.log(i)  // 6
```

上面是一个典型的面试题，给每个 `li` 标签绑定一个方法，点击时候执行。无论点击哪个 `li`，最终结果都是 6。这个也是代码执行时机问题，因为从头到尾只有一个 `i`，每次点击时候输出的 `i` 都是同一个，并且在点击时候 `i` 已经变成 6 了。所以只能输出 6。当然有人会说了，虽然从头到为只有一个 i，但是 i 是从 0 变化到 6 的呀，每次 i 变化为某一个值的时候就给 `li` 绑定一个函数，这时候 i 的值没有传入到这个函数吗？？？如果传入了，不就是点击第几个 `li` 输出几吗？额，只能说同学你很有想法。。。

下面请记住一句话：只有在函数调 fn 用时候，才会给函数 fn 内的 i 传入值，声明时候是不传值的。比如：

```javascript
var i = 1
function fn() {
 console.log(i)
}
i = 2
fn()  // 2
```

上面代码很好理解吧，fn 声明完毕时，i 还等于 1，但是 fn 执行时，i 已经变成了 2 。传给 fn 的 i 是 调用 fn 之前的2，而不是声明之前的 1 。这跟 `li` 上面的 fn 没有区别啊。如果实在不懂，那就把 for 循环拆解如下：

```javascript
for (var i = 0; i < liTags.length; i++) {  // liTags.length = 6
  liTags[i].onclick = function() {
    console.log(i)
  }
}
// 上面代码相当于下面

var i

i = 0 
liTags[0].onclick = function() {
  console.log(i)
}

i = 1 
liTags[1].onclick = function() {
  console.log(i)
}
 .
 .
 .
i = 5
liTags[5].onclick = function() {
  console.log(i)
}

i = 6
```

到目前为止，没有一个绑定在 `li` 上面的匿名函数执行。那么我们现在点击一个 `li` 就相当于给 `i=6`下面添加一行 `匿名函数()` 即匿名函数的执行，显然，输出 6。

但是我们的需求是，点击第几个 `li `就输出几啊，所以我们每个 `li` 绑定的函数的 `i` 不能是同一个。下面我们就想办法解决这个问题。

```javascript
var liTags = document.querySelectorAll('li')

for (var i = 0; i < liTags.length; i++) {  // liTags.length = 6
  var j = i
  liTags[j].onclick = function() {
    console.log(j)
  }
}
console.log(i)  // 6
```

我们再声明一个 j，让它记住每次循环 i 的值。可行吗？答案是否定的，因为 var 声明的变量会提升。所以实际执行的代码是下面

```javascript
var liTags = document.querySelectorAll('li')
var j
for (var i = 0; i < liTags.length; i++) {  // liTags.length = 6
  j = i
  liTags[j].onclick = function() {
    console.log(j)
  }
}
console.log(i,j)  // 6 5
```

实际上仍然只有一个全局作用域的 j。。。并没有构造出多个局部变量 j。

在 ES5 时代，我们想解决这个问题还真的不简单，方法就是立即执行函数

```javascript
var liTags = document.querySelectorAll('li')
for (var i = 0; i < liTags.length; i++) {  // liTags.length = 6
  (function() {
    var j = i
    liTags[j].onclick = function() {
      console.log(j)
    }
  }())
}
```

是不是很崩溃🤣😂。

但是 ES6 给我们带来了 let！let 不会变量提升！！所以有以下代码

```javascript
var liTags = document.querySelectorAll('li')
for (var i = 0; i < liTags.length; i++) {  // liTags.length = 6
  let j = i
  liTags[j].onclick = function() {
    console.log(j)
  }
}
console.log(i,j)  // j的作用域只到 for 循环的花括号，这里报错
```

简单吧，换了一种变量声明方式立马解决 ES5 的老大难。分析下原因：let 不会变量提升，所以循环执行了 6 次就声明了 6 个不同的 j，每个 `li` 绑定的函数的要打印的 j 都不是同一个。引申以下，6 次循环相当于构造了 6 个局部作用域，因为按照 let 的第三个特点，在同一个作用域下，不能重复使用 let 声明变量。for 循环 () 里面的 i 的作用域就在 () 里面，是循环体的父作用域。

ES6 有一个语法糖，困扰了我很久

```javascript
var liTags = document.querySelectorAll('li')
for (let i = 0; i < liTags.length; i++) {  // liTags.length = 6
  liTags[i].onclick = function() {
    console.log(i)
  }
}
```

上面的代码效果没有发生变化。第一次看时候我就纳闷了，i 不就声明了一次吗，怎么每次点击 `li` 打印的结果会不同呢？这就是 ES6 的一个语法糖了。上面的代码相当于下面

```javascript
var liTags = document.querySelectorAll('li')
for (let i = 0; i < liTags.length; i++) {  // liTags.length = 6
  let i = _i  // _i 代表()中 i 每次循环的值。ES6 自动加的
  liTags[i].onclick = function() {
    console.log(i)
  }
}
```

注意 for 循环 (..) 的 i 的作用域是在整个循环，循环体 {..} 内的是一个单独的作用域，(..) 相当于 {..} 的父作用域。

总结：

let 需要记住 上面 3 个特点和语法糖。如果语法糖实在不懂，那就死记硬背，反正会生成多个 i 就完事了。

参考：

- [我用了两个月的时间才理解 let](https://zhuanlan.zhihu.com/p/28140450)

