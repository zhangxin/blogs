# 字符串&JSON

## 常见的字符串方法

1. 长度计算,连接

```javascript
    var str = "hello";
    console.log( str.length );
    console.log( str[0] );
    console.log( str[str.length - 1]  );
    console.log( str.charAt(0) );    // 0 处的字符
    console.log( str.charCodeAt(0) );   // 某处字符的 unicode

    var str2 = " world";
    var str3 = str1 + str2;
	var str4 = str1.concat(str2) // 与 + 作用相同
    cosnole.log( str3 ); // hello world
    cosnole.log( str4 ); // hello world
```

2. 字符串截取

```javascript
    var str = "hello world";
    var sub1 = str.substr(1, 3); // 第一个是开始位置， 第二个是长度  ell
    var sub2 = str.substring(1, 3); // 第一个是开始位置，第二个是结束位置，长度为第二个减去第一个
    var sub3 = str.slice(1, 3); // 同上 允许负参
```

3. 查找

```javascript
    var str = "hello my world";
    var s1 = str.search('my');   //6 找不到为-1
    var s2 = str.replace('my', 'your'); //  替换
    var s3 = str.match('my'); //返回匹配的数组
	var index = str.indexOf("hello") // 0
    var index = str.indexOf("World") // -1 大小写敏感
```

4. 大小写

```javascript
    var str = "Hello";
    str.toUpperCase();
    str.toLowerCase();
```

5. 字符串切割成数组

```javascript
var str = "hello"
var strArray = str.split('')  // 将字符串按照参数为界切割成为数组
var newStr = strArray.join('') // 将字符数组按照参数拼接起来
```

字符串操作不会修改原来的字符串

## ES6新增的操作字符串的方法

1. 返回字符的 Unicode 码

```javascript
let s = '𠮷a';
s.codePointAt(0) // 134071
s.codePointAt(1) // 57271
s.codePointAt(2) // 97
```

`codePointAt` 方法的参数，是字符在字符串中的位置（从 0 开始）。上面代码中，JavaScript 将“𠮷a”视为三个字符，`codePointAt` 方法在第一个字符上，正确地识别了“𠮷”，返回了它的十进制码点 134071（即十六进制的20BB7）。在第二个字符（即“𠮷”的后两个字节）和第三个字符“a”上，`codePointAt` 方法的结果与`charCodeAt` 方法相同。

2. String.fromCodePoint()

ES5 提供 `String.fromCharCode` 方法，用于从码点返回对应字符，但是这个方法不能识别超过两字节的字符（Unicode 编号大于0xFFFF）。

```
String.fromCharCode(0x20BB7)
// "ஷ"
```

上面代码中，`String.fromCharCode`不能识别大于 `0xFFFF` 的码点，所以 `0x20BB7` 就发生了溢出，最高位 2 被舍弃了，最后返回码点 `U+0BB7` 对应的字符，而不是码点 `U+20BB7` 对应的字符。
ES6 提供了 `String.fromCodePoint` 方法，可以识别大于 `0xFFFF` 的字符，弥补了 `String.fromCharCode` 方法的不足。在作用上，正好与 `codePointAt` 方法相反。

```javascript
String.fromCodePoint(0x20BB7)
// "𠮷"
String.fromCodePoint(0x78, 0x1f680, 0x79) === 'x\uD83D\uDE80y'
// true
```

2. 字符串的遍历器接口 for of

```javascript
for (let codePoint of 'abc') {
  console.log(codePoint)
}
// "a"
// "b"
// "c"
```

除了遍历字符串，这个遍历器最大的优点是可以识别大于 `0xFFFF` 的码点，传统的 `for` 循环无法识别这样的码点。

4. at()

`at` 方法可以识别 Unicode 编号大于 `0xFFFF` 的字符，返回正确的字符。

```
‘abc’.at(0)//"a"
'吉'.at(0)//"吉"
```

5. normalize()

许多欧洲语言有语调符号和重音符号。为了表示它们，Unicode 提供了两种方法。一种是直接提供带重音符号的字符，比如 Ǒ（u01D1）。另一种是提供合成符号（combining character），即原字符与重音符号的合成，两个字符合成一个字符，比如 O（u004F）和 ˇ（u030C）合成 Ǒ（u004Fu030C）。

这两种表示方法，在视觉和语义上都等价，但是 JavaScript 不能识别。

```javascript
'\u01D1'==='\u004F\u030C' //false    
'\u01D1'.length // 1
'\u004F\u030C'.length // 2
```

上面代码表示，JavaScript 将合成字符视为两个字符，导致两种表示方法不相等。
ES6 提供字符串实例的 normalize() 方法，用来将字符的不同表示方法统一为同样的形式，这称为 Unicode 正规化。

```javascript
'\u01D1'.normalize() === '\u004F\u030C'.normalize()
// true
```

6. includes(), startsWith(), endsWith()

传统上，JavaScript 只有 indexOf 方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6 又提供了三种新方法。

```javascript
**includes()**：返回布尔值，表示是否找到了参数字符串。
**startsWith()**：返回布尔值，表示参数字符串是否在原字符串的头部。
**endsWith()**：返回布尔值，表示参数字符串是否在原字符串的尾部。
let s = 'Hello world!';    
s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
```

这三个方法都支持第二个参数，表示开始搜索的位置。

```javascript
let s = 'Hello world!';    
s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```

上面代码表示，使用第二个参数 n 时，`endsWith` 的行为与其他两个方法有所不同。它针对前 n 个字符，而其他两个方法针对从第 n 个位置直到字符串结束。

7. repeat()

`repeat` 方法返回一个新字符串，表示将原字符串重复n次。

```javascript
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""
```

参数如果是小数，会被取整。

```javascript
'na'.repeat(2.9) // "nana"
```

如果 `repeat`的参数是负数或者 `Infinity`，会报错。

```javascript
'na'.repeat(Infinity)
// RangeError
'na'.repeat(-1)
// RangeError
```

8. padStart()，padEnd()

ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。`padStart()`用于头部补全，`adEnd()` 用于尾部补全。

```javascript
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'

'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```

上面代码中，padStart 和 padEnd一共接受两个参数，第一个参数用来指定字符串的最小长度，第二个参数是用来补全的字符串。如果原字符串的长度，等于或大于指定的最小长度，则返回原字符串。

```javascript
'xxx'.padStart(2, 'ab') // 'xxx'
'xxx'.padEnd(2, 'ab') // 'xxx'
```

如果用来补全的字符串与原字符串，两者的长度之和超过了指定的最小长度，则会截去超出位数的补全字符串。

```javascript
'abc'.padStart(10, '0123456789')
// '0123456abc'
```

如果省略第二个参数，默认使用空格补全长度。

```javascript
'x'.padStart(4) // '   x'
'x'.padEnd(4) // 'x   '
```

`padStart` 的常见用途是为数值补全指定位数。下面代码生成 10 位的数值字符串。

```javascript
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"
'123456'.padStart(10, '0') // "0000123456"
```

另一个用途是提示字符串格式。

```javascript
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

9. matchAll()

`matchAll` 方法返回一个正则表达式在当前字符串的所有匹配。

10. 字符串模板

模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。----- 字符串模板，用到比较多。

```javascript
// 普通字符串
`In JavaScript '\n' is a line-feed.`

// 多行字符串
`In JavaScript this is
 not legal.`

console.log(`string text line 1
string text line 2`);

// 字符串中嵌入变量
let name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```

上面代码中的模板字符串，都是用反引号表示。如果在模板字符串中需要使用反引号，则前面要用反斜杠转义。

```javascript
let greeting = `\`Yo\` World!`;
```

如果使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中。

```javascript
$('#list').html(`
<ul>
  <li>first</li>
  <li>second</li>
</ul>
`);
```

上面代码中，所有模板字符串的空格和换行，都是被保留的，比如<ul>标签前面会有一个换行。如果你不想要这个换行，可以使用trim方法消除它。

```javascript
$('#list').html(`
<ul>
  <li>first</li>
  <li>second</li>
</ul>
`.trim());
```

模板字符串中嵌入变量，需要将变量名写在 `${}` 之中。

```javascript
function authorize(user, action) {
  if (!user.hasPrivilege(action)) {
    throw new Error(
      // 传统写法为
      // 'User '
      // + user.name
      // + ' is not authorized to do '
      // + action
      // + '.'
      `User ${user.name} is not authorized to do ${action}.`);
  }
}
```

大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性。

```javascript
let x = 1;
let y = 2;

`${x} + ${y} = ${x + y}`
// "1 + 2 = 3"

`${x} + ${y * 2} = ${x + y * 2}`
// "1 + 4 = 5"

let obj = {x: 1, y: 2};
`${obj.x + obj.y}`
// "3"
```

模板字符串之中还能调用函数。

```javascript
function fn() {
  return "Hello World";
}    
`foo ${fn()} bar`
// foo Hello World bar
```

如果大括号中的值不是字符串，将按照一般的规则转为字符串。比如，大括号中是一个对象，将默认调用对象的 `toString` 方法。
如果模板字符串中的变量没有声明，将报错。

```javascript
// 变量place没有声明
let msg = `Hello, ${place}`;
// 报错
```

由于模板字符串的大括号内部，就是执行 JavaScript 代码，因此如果大括号内部是一个字符串，将会原样输出。

```javascript
`Hello ${'World'}`
// "Hello World"
```

模板字符串甚至还能嵌套。

```javascript
const tmpl = addrs => `
  <table>
  ${addrs.map(addr => `
    <tr><td>${addr.first}</td></tr>
    <tr><td>${addr.last}</td></tr>
  `).join('')}
  </table>
`;
```

文中ES6的内容，主要来自于阮一峰的《ES6标准入门》。

## 对象

简单说，所谓对象，就是一种无序的数据集合，由若干个“键值对”（key-value）构成。

```javascript
var obj = {
  p: 'Hello World'
};
```

上面代码中，大括号就定义了一个对象，它被赋值给变量 `obj`。这个对象内部包含一个键值对（又称为“成员”），`p` 是“键名”（成员的名称），字符串 `Hello World`是“键值”（成员的值）。键名与键值之间用冒号分隔。如果对象内部包含多个键值对，每个键值对之间用逗号分隔。

```javascript
var o = {
  p1: 'Hello',
  p2: 'World'
};
```

`{key: value}` 是 JS 对象字面量写法

### 基本使用

```javascript
var company = {
    name: '小明',
    age: 3,
    sayHello: function(){
    console.log('hello world')
    }
}
console.log(company.name)
console.log(company['name'])
company.sayHello()

company.addr = '杭州市'
compay['business'] = '外贸'

for(var key in company){
    console.log(key)
    console.log(company[key])
}
```

### 详细介绍

#### 键名

对象的所有键名都是字符串，符合标识符的键名加不加引号都可以。上面的代码也可以写成下面这样。

```javascript
var o = {
  'p': 'Hello World'
};
```

如果键名是数值，会被自动转为字符串。

```javascript
var o ={
  1: 'a',
  3.2: 'b',
  1e2: true,
  1e-2: true,
  .234: true,
  0xFF: true
};

o
// Object {
//   1: "a",
//   3.2: "b",
//   100: true,
//   0.01: true,
//   0.234: true,
//   255: true
// }
```

但是，如果键名不符合标识名的条件（比如第一个字符为数字，或者含有空格或运算符），也不是数字，则必须加上引号，否则会报错。

```javascript
var o = {
  '1p': "Hello World",
  'h w': "Hello World",
  'p+q': "Hello World"
};
```

上面对象的三个键名，都不符合标识名的条件，所以必须加上引号。

> 总结：键名必须是字符串，符合标识符规则的键名和纯数字键名可以不加引号，其他的必须加

注意，JavaScript 的保留字可以不加引号当作键名。

```javascript
var obj = {
  for: 1,
  class: 2
};
```

#### 属性

对象的每一个“键名”又称为“属性”（property），它的“键值”可以是任何数据类型。如果一个属性的值为函数，通常把这个属性称为“方法”，它可以像函数那样调用。

```javascript
var o = {
  p: function (x) {
    return 2 * x;
  }
};

o.p(1)
// 2
```

上面的对象就有一个方法 `p`，它就是一个函数。

对象的属性之间用逗号分隔，最后一个属性后面可以加逗号（trailing comma），也可以不加。

```javascript
var o = {
  p: 123,
  m: function () { ... },
}
```

上面的代码中 `m` 属性后面的那个逗号，有或没有都不算错。

属性可以动态创建，不必在对象声明时就指定。

```javascript
var obj = {};
obj.foo = 123;
obj.foo // 123
```

上面代码中，直接对 `obj` 对象的 `foo` 属性赋值，结果就在运行时创建了 `foo` 属性。

### 对象的引用

如果不同的变量名指向同一个对象，那么它们都是这个对象的引用，也就是说指向同一个内存地址。修改其中一个变量，会影响到其他所有变量。

```javascript
var o1 = {};
var o2 = o1;

o1.a = 1;
o2.a // 1

o2.b = 2;
o1.b // 2
```

上面代码中，`o1` 和 `o2` 指向同一个对象，因此为其中任何一个变量添加属性，另一个变量都可以读写该属性。

此时，如果取消某一个变量对于原对象的引用，不会影响到另一个变量。

```javascript
var o1 = {};
var o2 = o1;

o1 = 1;
o2 // {}
```

上面代码中，`o1` 和 `o2` 指向同一个对象，然后 `o1` 的值变为 1，这时不会对 `o2 `产生影响，`o2` 还是指向原来的那个对象。

但是，这种引用只局限于对象，对于原始类型的数据则是传值引用，也就是说，都是值的拷贝。

```javascript
var x = 1;
var y = x;

x = 2;
y // 1
```

上面的代码中，当 `x` 的值发生变化后，`y` 的值并不变，这就表示 `y` 和 `x` 并不是指向同一个内存地址。

### 属性的操作

#### 读取属性

读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符。

```javascript
var o = {
  p: 'Hello World'
};

o.p // "Hello World"
o['p'] // "Hello World"
```

上面代码分别采用点运算符和方括号运算符，读取属性 `p`。

请注意，如果使用方括号运算符，键名必须放在引号里面，否则会被当作变量处理。但是，数字键可以不加引号，因为会被当作字符串处理。

```javascript
var o = {
  0.7: 'Hello World'
};

o['0.7'] // "Hello World"
o[0.7] // "Hello World"
```

方括号运算符内部可以使用表达式。

```javascript
o['hello' + ' world']
o[3 + 3]
```

数值键名不能使用点运算符（因为会被当成小数点），只能使用方括号运算符。

```javascript
obj.0xFF
// SyntaxError: Unexpected token
obj[0xFF]
// true
```

上面代码的第一个表达式，对数值键名 `0xFF` 使用点运算符，结果报错。第二个表达式使用方括号运算符，结果就是正确的。

> 总结：点运算符只适合合法标识符。[] 运算符适合所有类型的键名，[] 里的非纯数字键名一定要加上引号，因为不加引号会被当做一个变量名处理，比如 `for...in` 循环中的 `obj[key]`。纯数字键名除外，会自动加上引号。

#### 检查变量是否声明

如果读取一个不存在的键，会返回 `undefined`，而不是报错。可以利用这一点，来检查一个全局变量是否被声明。

```javascript
// 检查a变量是否被声明
if (a) {...} // 报错

if (window.a) {...} // 不报错
if (window['a']) {...} // 不报错
```

上面的后二种写法之所以不报错，是因为在浏览器环境，所有全局变量都是 `window` 对象的属性。`window.a` 的含义就是读取 `window` 对象的 `a` 属性，如果该属性不存在，就返回 `undefined`，并不会报错。

需要注意的是，后二种写法有漏洞，如果 `a` 属性是一个空字符串（或其他对应的布尔值为 `false` 的情况），则无法起到检查变量是否声明的作用。正确的做法是可以采用下面的写法。

```javascript
if ('a' in window) {
  // 变量 a 声明过
} else {
  // 变量 a 未声明
}
```

#### 属性的赋值

点运算符和方括号运算符，不仅可以用来读取值，还可以用来赋值。

```javascript
o.p = 'abc';
o['p'] = 'abc';
```

上面代码分别使用点运算符和方括号运算符，对属性 p 赋值。

JavaScript 允许属性的“后绑定”，也就是说，你可以在任意时刻新增属性，没必要在定义对象的时候，就定义好属性。

```javascript
var o = { p: 1 };

// 等价于

var o = {};
o.p = 1;
```

#### 查看所有属性

查看一个对象本身的所有属性，可以使用`Object.keys`方法。

```javascript
var o = {
  key1: 1,
  key2: 2
};

Object.keys(o);
// ['key1', 'key2']
```

#### delete命令

`delete`命令用于删除对象的属性，删除成功后返回`true`。

```javascript
var o = {p: 1};
Object.keys(o) // ["p"]

delete o.p // true
o.p // undefined
Object.keys(o) // []
```

上面代码中，`delete` 命令删除 `o` 对象的 `p` 属性。删除后，再读取 `p` 属性就会返回 `undefined`，而且 `Object.keys` 方法的返回值中，`o `对象也不再包括该属性。

注意，删除一个不存在的属性，`delete` 不报错，而且返回 `true`。

```javascript
var o = {};
delete o.p // true
```

上面代码中，`o ` 对象并没有 `p` 属性，但是 `delete` 命令照样返回 `true`。因此，不能根据 `delete`  命令的结果，认定某个属性是存在的，只能保证读取这个属性肯定得到 `undefined`。

`delete` 命令不能删除 `var` 命令声明的变量，只能用来删除属性。

```javascript
var p = 1;
delete p // false
delete window.p // false
```

上面命令中，`p `是 `var` 命令声明的变量，`delete `命令无法删除它，返回 `false`。因为 `var` 声明的全局变量都是顶层对象的属性，而且默认不得删除。

#### for...in循环

`for...in`循环用来遍历一个对象的全部属性。

```javascript
var o = {a: 1, b: 2, c: 3};

for (var i in o) {
  console.log(o[i]);
}
// 1
// 2
// 3
```

## JSON

### JSON 格式

JSON 格式（JavaScript Object Notation 的缩写）是一种轻量级的数据交换格式，2001年由 Douglas Crockford 提出，目的是取代繁琐笨重的 XML 格式。易于人阅读和编写。同时也易于机器解析和生成。 它不是 JS 对象语法的一个子集，JSON 采用完全独立于语言的文本格式，但是也使用了类似于 C 语言家族的习惯（包括 C, C++, C#, Java, JavaScript, Perl, Python 等）。这些特性使 JSON 成为理想的数据交换语言。

JSON 对值的类型和格式有严格的规定。

1. 复合类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象。
2. 简单类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和 `null`（不能使用`NaN`, `Infinity`, `-Infinity`和`undefined`）。
3. 字符串必须使用双引号表示，不能使用单引号。
4. 对象的键名必须放在双引号里面。
5. 数组或对象最后一个成员的后面，不能加逗号。

以下是合格的 JSON 值。

```javascript
["one", "two", "three"]

{ "one": 1, "two": 2, "three": 3 }

{"names": ["张三", "李四"] }

[ { "name": "张三"}, {"name": "李四"} ]
```

以下是不合格的 JSON 值。

```javascript
{ name: "张三", 'age': 32 }  // 属性名必须使用双引号

[32, 64, 128, 0xFFF] // 不能使用十六进制值

{ "name": "张三", "age": undefined } // 不能使用undefined

{ "name": "张三",
  "birthday": new Date('Fri, 26 Aug 2011 07:13:10 GMT'),
  "getName": function() {
      return this.name;
  }
} // 不能使用函数和日期对象
```

需要注意的是，空数组和空对象都是合格的 JSON 值，`null` 本身也是一个合格的 JSON 值。

ES5 新增了`JSON`对象，用来处理 JSON 格式数据。它有两个方法：`JSON.stringify()`和`JSON.parse()`。

### JSON.stringify()

#### 基本用法

`JSON.stringify` 方法用于将一个值转为字符串。该字符串符合 JSON 格式，并且可以被 `JSON.parse` 方法还原。

```javascript
JSON.stringify('abc') // ""abc""
JSON.stringify(1) // "1"
JSON.stringify(false) // "false"
JSON.stringify([]) // "[]"
JSON.stringify({}) // "{}"

JSON.stringify([1, "false", false])
// '[1,"false",false]'

JSON.stringify({ name: "张三" })
// '{"name":"张三"}'
```

上面代码将各种类型的值，转成 JSON 字符串。其实是将一个 JS 值转换为符合 JSON 格式的 JS 字符串，本质还是 JS 字符串。字符串引号内的值符合 JSON 格式。

需要注意的是，对于原始类型的字符串，转换结果会带双引号。

```javascript
JSON.stringify('foo') === "foo" // false
JSON.stringify('foo') === "\"foo\"" // true
JSON.stringify('foo') === ''"foo"' // true
```

上面代码中，字符串`foo`，被转成了 `""foo""`。这是因为将来还原的时候，双引号可以让  JavaScript 引擎知道，`foo` 是一个字符串，而不是一个变量名。

如果原始对象中，有一个成员的值是 `undefined`、函数或 XML 对象等不符合非 JSON 值，这个成员会被过滤。

```javascript
var obj = {
  a: undefined,
  b: function () {}
};

JSON.stringify(obj) // "{}"
```

上面代码中，对象 `obj` 的 `a` 属性是 `undefined`，而 `b` 属性是一个函数，结果都被 `JSON.stringify` 过滤。

如果数组的成员是 `undefined`、函数或 XML 对象，则这些值被转成 `null`。

```javascript
var arr = [undefined, function () {}];
JSON.stringify(arr) // "[null,null]"
```

上面代码中，数组 `arr` 的成员是 `undefined` 和函数，它们都被转成了 `null`。

正则对象会被转成空对象。

```javascript
JSON.stringify(/foo/) // "{}"
```

`JSON.stringify` 方法会忽略对象的不可遍历属性。

### JSON.parse()

`JSON.parse`方法用于将 JSON 字符串转化成 JS 值。

```javascript
JSON.parse('{}') // {}
JSON.parse('true') // true
JSON.parse('"foo"') // "foo"
JSON.parse('[1, 5, "false"]') // [1, 5, "false"]
JSON.parse('null') // null

var o = JSON.parse('{"name": "张三"}');
o.name // 张三
```

如果传入的字符串不是有效的 JSON 格式，`JSON.parse` 方法将报错。

```javascript
JSON.parse("'String'") // illegal single quotes
// SyntaxError: Unexpected token ILLEGAL
```

上面代码中，双引号字符串中是一个单引号字符串，因为单引号字符串不符合 JSON 格式，所以报错。

### 深拷贝的另一种写法

```
var obj = {
    name: 'hunger',
    age: 3,
    friends: ['aa', 'bb', 'cc']
}

var obj2 = JSON.parse(JSON.stringify(obj))
obj.age = 4
console.log(obj2.age)
```

上面的写法其实也有问题，如果对象的一个成员是函数那么它就会被过滤，就不能正确的拷贝

### JavaScript 对象和 JSON 的关系

JavaScript 对象的字面量写法只是长的像 JSON 格式数据，二者属于不同的范畴，JavaScript 对象中很多类型(函数、正则、Date) JSON 格式的规范并不支持，JavaScript 对象的字面量写法更宽松。

## 一个会误导人的现象

```javascript
var a = JSON.stringify('abc')  // a = ""abc""
JSON.parse(""abc"")  // 报错 VM256:1 Uncaught SyntaxError: missing ) after argument list
JSON.parse(a)  // "abc"
JSON.parse('"abc"')  // "abc"
JSON.parse("'abc'") 

/*
uncaught SyntaxError: Unexpected token ' in JSON at position 0
    at JSON.parse (<anonymous>)
    at <anonymous>:1:6
 */
```

由于 JSON 的 String 必须采用双引号，而 JS 的 String  单双都可，所以在遇到字符串的时候 `var a = JSON.stringify('abc') ` 实际转换出的为 `'"abc"'`，只是由于控制台经常显示为 `""abc""` ，会让人以为结果就是它，其实本质还是合法的 JS 字符串，只是里面的引号必须是双引号，因为 `a` 还是一个 JS 字符串，要符合 JS 语法。

总结：`JSON.stringify()` 的返回值必须是一个合法的 JS 字符串，字符串的值符合 JSON 格式。`JSON.parse()` 的参数必须是一个合法的 JS 字符串，字符串的值符合 JSON 格式。

## 参考链接

- 以上大量参考 [阮一峰 javascript 教程](http://javascript.ruanyifeng.com/stdlib/json.html)
- 推荐阅读 [JSON 是什么](http://blog.jirengu.com/?p=378)
