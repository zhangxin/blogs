# Math

## Math

Math 对象是 JavaScript 的内置对象，提供一系列数学常数和数学方法。Math 对象只提供了静态的属性和方法，所以使用时不用实例化

### 属性

Math 对象提供以下一些只读的数学常数。

```javascript
Math.E // 2.718281828459045
Math.LN2 // 0.6931471805599453
Math.LN10 // 2.302585092994046
Math.LOG2E // 1.4426950408889634
Math.LOG10E // 0.4342944819032518
Math.PI // 3.141592653589793
Math.SQRT1_2 // 0.7071067811865476
Math.SQRT2 // 1.4142135623730951
```

### 方法

- round：用于四舍五入

```javascript
Math.round(0.1) // 0
Math.round(0.5) // 1
```

它对于负值的运算结果与正值略有不同，主要体现在对.5的处理

```javascript
Math.round(-1.1) // -1
Math.round(-1.5) // -1
```

- abs，max，min

abs 方法返回参数值的绝对值

```javascript
Math.abs(1) // 1
Math.abs(-1) // 1
```

max 方法返回最大的参数，min 方法返回最小的参数

```javascript
Math.max(2, -1, 5) // 5
Math.min(2, -1, 5) // -1
```

- floor，ceil

floor 方法返回小于参数值的最大整数

```javascript
Math.floor(3.2) // 3
Math.floor(-3.2) // -4
```

ceil 方法返回大于参数值的最小整数

```javascript
Math.ceil(3.2) // 4
Math.ceil(-3.2) // -3
```

- pow，sqrt

pow 方法返回以第一个参数为底数、第二个参数为幂的指数值

```javascript
Math.pow(2, 2) // 4
Math.pow(2, 3) // 8
```

sqrt 方法返回参数值的平方根。如果参数是一个负值，则返回 NaN

```javascript
Math.sqrt(4) // 2
Math.sqrt(-4) // NaN
```

- log，exp

log 方法返回以e为底的自然对数值

```javascript
Math.log(Math.E) // 1
Math.log(10) // 2.302585092994046
```

求以 10 为底的对数，可以除以 Math.LN10；求以 2 为底的对数，可以除以 Math.LN2。

```javascript
Math.log(100)/Math.LN10 // 2
Math.log(8)/Math.LN2 // 3
```

exp 方法返回常数e的参数次方

```javascript
Math.exp(1) // 2.718281828459045
Math.exp(3) // 20.085536923187668
```

- random

该方法返回 0 到 1 之间的一个伪随机数，可能等于 0，但是一定小于 1

Math.random() // 0.7151307314634323

这个最常用，其他用的不多

```javascript
// 返回给定范围内的随机数
function getRandomArbitrary(min, max) {
  return Math.random() * (max - min) + min;
}

// 返回给定范围内的随机整数
function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

- 三角函数

sin 方法返回参数的正弦，cos 方法返回参数的余弦，tan 方法返回参数的正切。参数是弧度

```javascript
Math.sin(0) // 0
Math.cos(0) // 1
Math.tan(0) // 0
```

asin 方法返回参数的反正弦，acos 方法返回参数的反余弦，atan 方法返回参数的反正切。这三个方法的返回值都是弧度值。

```javascript
Math.asin(1) // 1.5707963267948966
Math.acos(1) // 0
Math.atan(1) // 0.7853981633974483
```
