# unit1
- JavaScript包括三部分：
  - ECMAScript:提供核心语言功能
  - 文档对象模型(DOM):提供访问和操作网页内容的方法和接口
  - 浏览器对象模型(BOM):提供与浏览器交互的方法和接口

# unit2
### \<script> 元素
  - 作用：在HTML中插入JavaScript
  - 属性（6个，主要用下面4个）
    - async：异步的，表示立即下载脚本，但不妨碍页面中的其他操作，只对外部文件有效
    - defer：表示脚本可以延迟到文档完全解析和显示之后再执行，只对外部文件有效
    - src：要引入外部文件的路径，可以是与包含该脚本的页面位于同一个服务器上的文件，也可以是其他任何域中的文件
    - type：text/javascript
- 特点:
  - `<script>`标签后的页面，会在脚本完全执行后才显示，如果js执行时间过长，就会出现白屏现象。

# unit3
### 数据类型(3 + 2 + 1)
  - 5种基本数据类型
    - Undefined：定义了一个变量，但是没初始化，它的值就为undefined(小写)
    - Null：空对象指针，意在保存对象但是还未真正保存对象，它的值就为null(小写)
    - Boolean
    - Number
    - String
  - 1种复杂数据类型
    - Object
      - 对象是最复杂的数据类型，又可以分成三个子类型。
        - 狭义的对象（object）
        - 数组（array）
        - 函数（function）
### typeof操作符
  - 判断变量的数据类型，6种返回值(undefined,boolean,number,string,object,function)
  - type是操作符，后跟变量名或者字面量
  - typeof null  返回 "object"
### Undefined 和 Null 注意事项
  - console.log(null == undefined) //返回true, "=="操作符在比较时会转换操作数
  - typeof null (返回 "object")，typeof undefined (返回 "undefined")
### Boolean
  - Boolean()，数据类型转换函数，可接收任意类型的参数
### Number
  - NaN(Not a Number)
    - 任何涉及NaN的操作都会返回NaN
    - NaN与任何值都不相等，包括他本身
  - 数据类型转换函数(3个，P30~P32)
    - Number():可接收任意类型的参数
      - 空字符串返回0
    - parseInt()：只转换字符串
    - parseFloat()：同上
      - 上面两个空字符串都返回NaN
### String
  - 数据类型转换函数(2个，P34)
    - toString()
      - undefined 和 null值没有toString方法
      - 多数情况下，调用toString()方法不必传入参数，但是，调用数值的toString()方法时，可以传入一个参数：输出数值的基数
      ```
      var num = 10;
      alert(num.toString());      //  "10"
      alert(num.toString(2));     //  "1010"
      alert(num.toString(8));     //  "12"
      alert(num.toString(10));    //  "10"
      alert(num.toString(16));    //  "a"
      ```
    - String()
      - 可以把null转换为"null",undefined转换为"undefined"
      ```
      String(null)          // "null"
      String(undefined)     // "undefined"
      ```
    - "" + 要转换的值
      
      - 与 String()功能一样
### 操作符
  > JS的操作符遵守一个法则，当操作符和操作数类型不匹配时，会进行数据类型转换
  - "++ -- + -"
    
    - 这四个操作符可以用在任意类型，用在非数值类型时，会先进行类型转换
  - 位操作
    - \>> 无符号右移操作符
      - 正数进行无符号右移的操作时，与有符号右移\>>结果相同
      - 负数进行无符号右移的操作时，会把负数的**补码**当作**纯二进制**码进行解析，所以得到的数值会非常大
      ```
        var oldValue = -64; // 11111111111111111111111111000000
        var newValue = oldValue >>> 5;  // 13421726
      ```
  - 布尔操作(P44~P46)
    - !
      - 可以用于任何值,都会返回布尔值
      - 常用于进行数据类型转换，`!! a` 与 `Boolean(a)` 效果相同 
    - &&
      - 有一个操作数不是布尔类型时，该操作不一定返回布尔值 (6种情况) 
        - 第一个操作数是对象，返回第二个操作数
        - 第二个操作数是对象，第一个操作数的求值结果为true时，返回该对象
        - 两个操作数都是对象，返回第二个操作数
        - 第一个操作数是null，返回null
        - 第一个操作数是NaN，返回NaN
        - 第一个操作数是undefined，返回undefined
    - ||
      - 有一个操作数不是布尔类型时，该操作不一定返回布尔值 (6种情况)
        - 第一个操作数是对象，返回第一个操作数
        - 第一个操作数的求值结果为false时，返回第二个操作数
        - 两个操作数都是对象，返回第一个操作数
        - 两个操作数是null，返回null
        - 两个操作数是NaN，返回NaN
        - 两个操作数是undefined，返回undefined
      - 用逻辑或的性质避免为变量赋值为null或undefined值，如：
        ```
        var myObj = pre || bac
        ```
      > myObj将会被赋值为等号后面两个值的其中一个，优先pre，bac为后备
  - 乘性操作符(* / %)
    - 操作符为非数值时会进行数据类型转换
    - 0和`Infinity`相乘得到`NaN`
    - `Infinity`和`Infinity`相乘得到 `Infinity`
    - `Infinity`和非0数值相乘得到`Infinity`或`-Infinity`
    - `Infinity`和`Infinity`相乘得到 `NaN`
  - 加性运算符
    - " + "的三个作用
      - 算术运算
      - 数据类型转换，作用类似Number()
      - 连接字符串
  - 关系操作符(\> , \< , <=， >=)
    - 如果两个操作符都是字符串，比较两个字符串相应的字符编码值，得到一个布尔值
    - 除了上面的情况，如果操作数不是数值，都将进行数据类型转换，转换成数值后再进行比较
    - 任何操作数与`NaN`比较都会得到`false`
  - 相等操作符
    - 相等和不相等(== , !=)
      - 先转换操作数的数据类型，再进行比较
      - 如果两个操作数都是对象，则比较它们是不是同一个对象，如果只有一个操作数是对象，则应调用对象的的valueof()方法后再进行比较
      - `null`和`undefined`相等
      - 比较相等性之前，不能转换`null`和`undefined`的类型
      - 一个操作数是`NaN`，相等操作符返回`false`，不等操作符返回`true`,两个操作数都是`NaN`，相等操作符返回`true`，不等操作符返回`false`
      ```
        undefined == 0      // false
        null == 0       // false
      ```
    - 全等和非全等(=== , !==)
      
      - 仅比较而不转换操作数的数据类型
### for-in 语句
  - 用来枚举对象的属性
  ```
    for (pro in obj)
      statement
  ```
### 函数参数
  - JS不介意传入函数参数的个数及数据类型，即使定义函数时只接收两个参数，但是调用时候可以传入0个或多个参数。
  - JS接收的参数实际是一个参数数组，JS接收的始终是一个数组，而不关心数组中到底有多少个参数。
  - 在函数内部可以通过`arguments`对象访问参数数组，从而获取传递给函数的每一个参数
  - `arguments`是一个类数组对象，`arguments`对象的长度是由调用函数时传入的参数决定的，不是定义函数时的参数个数决定的

# unit 4
- 检测类型
  - typeof：用于检测基本数据类型
  - instanceof ：用于检测一个操作数是哪种类型的对象
  ```
  result = ele instanceof Array || Object || RegExp
  ```
# unit 5
### Object类型
  - 声明一个对象有两种方法
    - 构造函数法
    ```
    var person = new Object();
    person.name = "xxx";
    person.name = 18;
    ```
    - 通过字面量
    ```
    var person = {
      name : "xxx",
      age : 18
    };
    ```
    > 注意，使用对象字面量表示法声明对象时候，不同属性应该用**逗号**隔开，最后一个属性后面没有逗号
    
  - 访问一个属性时，可以用点表示法和方括号表示法
    
      ```
      person["name"] = "xxx";
      ```
    - 好处：使用方括号表示法，可以通过变量访问属性；如果属性名中包含会导致语法错误的字符，或者属性名使用的是关键字或保留字，也可以通过方括号表示法
    ```
    var prn = "name";
    person[prn];
    ```
### Array类型 
  - 创建数组
    - 构造函数
      ```
      var cc = new Array(3); //注意：当传入的参数是数字n时，表示创建一个长度为n的数组

      var cc = new Array("a", "b", "c"); //注意：当传入的参数是字符串时，表示创建的数组的值为传入的参数
      ```
      - 数组字面量  
        ```
        var color = ["red", "black", "blue"];//注意：是 [] 不是 {}
        ```

  - JS中Array类型的几个特点
    - 同一个数组中可以保存任何类型的数据
    - 数组的大小是动态变化的：即没有数组越界，数组下标超过数组长度时，数组长度会自动变长
      - 一个小应用：在数组末尾不断添加新项
      ```
      var color = ["red", "black", "blue"];
      color[color.length] = "green";
      color[color.length] = "white";
      ```
    - 数组的length属性不是只读的，可以通过设置length的值，从数组的末尾移除项或者向数组中添加项
  - 常用方法
    - 检测数组的函数
      - Array.isArray()  
      - 作用：确定某个值是不是数组，不考虑该值是在哪个全局作用域中创建的
    - 转换方法
      - toString()：  返回由数组中的每个值的字符串形式拼接而成的一个以**逗号**分隔的字符串
      - toLocaleString()：同上
      - valueOf()：  返回数组本身
      - join()：指定一个分隔符来拼接一个字符串
    - 栈方法（先进后出）
      - push()：接受任意类型的参数，逐个添加到数组的末尾，并返回新数组的长度
      - pop()：从数组的末尾移除最后一项，减少数组的长度，返回被移除的项
    - 队列方法（先进先出）
      - push()
      - shift()：移除数组的第一项并返回该项的值，同时将数组长度减 1
      - unshift()：再数组前端条件任意个项并返回新数组的长度
    - 排序方法
      - reverse()：反转数组
      - sort()：将数组中的值按照升序排列
        - sort()函数在没有参数时，排的是字符而不是数组中数值的大小
        - 可以给sort()函数中传入一个compare()函数，就可以进行正常的数值大小的排序，可以通过改变compare()函数，让数组中的值降序排列
        ```
        function compare(num1, num2){
          if (num1 < num2){
            return -1;
          } else if (num1 > num2){
            return 1;
          } else {
            return 0;
          }
        }  // 升序，降序排列只需要将return的值改为 1， -1， 0
        ```


        // compare()函数可以简写为
        
        function compare(num1, num2){
          return num1 - num2;  //升序
        }
    
        ```
    
    - 操作方法(3个)
      - concat()：将传入的参数和原数组连接成一个新数组，返回值为新数组，不改变原数组。在没有传入参数时，只是返回一个原数组的副本
      - slice()：基于当前数组中的一个或多个项创建一个新数组。接收一个或两个参数，**不改变原数组**
        - 接收两个参数时，返回起始位置和结束位置之间的项（不包括结束位置）。如array.slice(a,b)，返回位置a到b之间共 b-a 项
        - 接收一个参数时，返回起始位置到数组末尾的项
      - splice()：**改变原素组**，返回值为一个数组，包含被删除的项
        - 删除：指定两个参数，要删除的第一项的位置和要删除的项数
        - 插入：向指定位置插入任意数量的项，提供3个参数（起始位置，0，要插入的项。如果要插入多个项，可以传入第四，第五等任意个项）
        - 替换：可以向指定位置插入任意数量的项，同时删除任意数量的项。传入3个参数（起始位置，要删除的项数，要插入的任意个项）
    
    - 位置方法（2个）
      - 都是接收两个参数：要查找的项和表示查找起点位置的索引 
      - indexOf()：从头查向尾查找
      - lastIndexOf()： 从尾向头查找
    - 迭代方法（5个）[p96]
      - every()
      - filter()
      - forEach()
      - map()
      - some()
    - 归并方法
      - reduce()
      - reduceRight()

### Function()类型 

