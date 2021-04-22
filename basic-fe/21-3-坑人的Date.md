# Date

## 时间的表示方式

### GMT

是指位于英国伦敦郊区的皇家格林尼治天文台当地的标准时间，因为本初子午线被定义为通过那里的经线。

自1924年2月5日开始，格林尼治天文台负责每隔一小时向全世界发放调时信息。

理论上来说，格林尼治标准时间的正午是指当太阳横穿格林尼治子午线时（也就是在格林尼治上空最高点时）的时间。但由于地球在它的椭圆轨道里的运动速度不均匀，这个时刻可能与实际的太阳时有误差，最大误差达 16 分钟。原因在于地球每天的自转是有些不规则的，而且正在缓慢减速，因此格林尼治时间基于天文观测本身的缺陷，已经被原子钟报时的协调世界时（UTC）所取代。

[参考](http://zh.wikipedia.org/wiki/GMT)

### UTC

协调世界时（英语：Coordinated Universal Time，法语：Temps Universel Coordonné，简称UTC）是最主要的世界时间标准，其以原子时秒长为基础，在时刻上尽量接近于格林尼治标准时间。中华民国采用 CNS 7648 的《资料元及交换格式–资讯交换–日期及时间的表示法》（与ISO 8601类似）称之为世界协调时间。中华人民共和国采用 ISO 8601:2000 的国家标准 GB/T 7408-2005《数据元和交换格式 信息交换 日期和时间表示法》中亦称之为协调世界时

[参考](https://zh.wikipedia.org/wiki/协调世界时)

### CST

北京时间，又名中国标准时间，是中国大陆的标准时间，比世界协调时快八小时（即UTC+8），与香港、澳门、台北、吉隆坡、新加坡等地的标准时间相同。

[参考](https://zh.wikipedia.org/wiki/CST)

## Javascript 中的 Date

```javascript
var d = new Date()
console.log(d.toString())   //"Wed Feb 28 2018 17:18:26 GMT+0800 (CST)"
console.log(d.toGMTString()) //"Wed, 28 Feb 2018 09:18:26 GMT"
console.log(d.toUTCString())  //"Wed, 28 Feb 2018 09:18:26 GMT"
console.log(d.toISOString()) //"2018-02-28T09:18:26.967Z"
console.log(d.toLocalString()) 

d.getTime()         //返回实例对象距离1970年1月1日00:00:00对应的毫秒数
d.getDate()         //返回实例对象对应每个月的几号（从1开始）
d.getDay()          //返回星期，星期日为0，星期一为1，以此类推
d.getFullYear()     //返回四位的年份
d.getMonth()        //返回月份（0表示1月，11表示12月）
d.getHours()        //返回小时(0~23)
d.getMilliseconds() //返回毫秒（0-999）
d.getMinutes()      //返回分钟（0-59）
d.getSeconds()      //返回秒（0-59）

var d2 = new Date()
d2.setDate()
d2.setDate(date)：设置实例对象对应的每个月的几号（1-31），返回改变后毫秒时间戳
d2.setFullYear(year [, month, date])：设置四位年份
d2.setHours(hour [, min, sec, ms])：设置小时（0-23）
d2.setMilliseconds()：设置毫秒（0-999）
d2.setMinutes(min [, sec, ms])：设置分钟（0-59）
d2.setMonth(month [, date])：设置月份（0-11）
d2.setSeconds(sec [, ms])：设置秒（0-59）
d2.setTime(milliseconds)：设置毫秒时间戳
```

## Date() 构造函数

使用 `Date()` 构造函数创建一个 Date 的实例，一共有四种形式

### 1. 没有参数

如果没有提供参数，那么新创建的 Date 对象表示当前代码执行时刻的日期和时间。

```javascript
var d = new Date()
```

### 2. Unix 时间戳

#### new Date(milliseconds)

Date 对象接受从 1970年1月1日00:00:00 UTC 开始计算的毫秒数作为参数。这意味着如果将 Unix 时间戳作为参数，必须将 Unix 时间戳乘以 1000。

一个 Unix 时间戳（[Unix Time Stamp](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_16)），它是一个整数值，表示自 1970年1月1日00:00:00 UTC（the Unix epoch）以来的毫秒数，忽略了闰秒。

```javascript
new Date(1378218728000); // Tue Sep 03 2013 22:32:08 GMT+0800 (CST)

// 1970年1月2日的零时
var Jan02_1970 = new Date(3600*24*1000); // Fri Jan 02 1970 08:00:00 GMT+0800 (CST)
```

### 3. dateString

#### new Date(datestring)

`Date()` 构造函数还接受一个日期字符串作为参数，返回所对应时间的时间对象。所有可以被 Date.parse() 方法解析的日期字符串，都可以当作 `Date()` 构造函数的参数。

**注意:** 由于浏览器之间的差异与不一致性，强烈不推荐使用 ``Date()` 构造函数来解析日期字符串 (或使用与其等价的 `Date.parse`)。对 RFC 2822 格式的日期仅有约定俗称的支持。 对 ISO 8601 格式的支持中，仅有日期的串 (例如 "1970-01-01") 会被处理为 UTC 而不是本地时间，与其他格式的串的处理不同。

```javascript
new Date("2013-02-15")
new Date("2013-FEB-15")
new Date("FEB, 15, 2013")
new Date("FEB 15, 2013")
new Date("Feberuary, 15, 2013")
new Date("Feberuary 15, 2013")
new Date("15, Feberuary, 2013")
```

#### 4. 分别提供日期与时间的每一个成员

#### new Date(year, month [, day, hours, minutes, seconds, ms])

在多个参数的情况下，`Date()` 构造函数将其分别视作对应的年、月、日、小时、分钟、秒和毫秒。如果采用这种用法，最少需要指定两个参数（年和月），其他参数都是可选的，默认等于 0。如果只使用一个参数，`Date()` 构造函数会将其解释为毫秒数。

```javascript
new Date(2013) // Thu Jan 01 1970 08:00:02 GMT+0800 (CST)
new Date(2013,0) // Tue Jan 01 2013 00:00:00 GMT+0800 (CST)
new Date(2013,0,1) // Tue Jan 01 2013 00:00:00 GMT+0800 (CST)
new Date(2013,0,1,0) // Tue Jan 01 2013 00:00:00 GMT+0800 (CST)
new Date(2013,0,1,0,0,0,0) // Tue Jan 01 2013 00:00:00 GMT+0800 (CST)
```

上面代码（除了第一行）返回的是 2013 年 1 月 1 日零点的时间，可以看到月份从 0 开始计算，因此 1月是 0，12 月是 11。但是，月份里面的天数从 1 开始计算。

## 静态方法

### Date.now()

now方法返回当前距离 `1970年1月1日00:00:00` （UTC 时间）的毫秒数（时间戳）。

```
Date.now(); // 1427974222853
```

### Date.parse()

`Date.parse()` 方法用来解析日期字符串，返回距离 `1970年1月1日 00:00:00` 的毫秒数（时间戳）

日期字符串的格式应该完全或者部分符合 `YYYY-MM-DDTHH:mm:ss.sssZ` 格式，Z 表示时区，是可选的

如果解析失败，返回 `NaN`

```
Date.parse("January 26, 2011 13:51:50")
Date.parse("Mon, 25 Dec 1995 13:30:00 GMT")
Date.parse("Mon, 25 Dec 1995 13:30:00 +0430")
Date.parse("2011-10-10")
Date.parse("2011-10-10 20:00:00")
Date.parse("2011-10-10T14:48:00")
```

## 获取时间戳的方式

1. Date.now()
2. Date.parse(dateString)
3. dater.getTime() 方法  // dater 是一个时间对象

## 注意事项

在新建日期对象时，如果不设置时间，则认为创建的是 utc 的 0点，也就是北京时间 8 点。 如果设置时间，则是北京时间当前时间。

```javascript
new Date('2018-01-01')  // Mon Jan 01 2018 08:00:00 GMT+0800 (CST)
new Date('2018-01-01 00:00:00')  //Mon Jan 01 2018 00:00:00 GMT+0800 (CST)
```

原生的 Date 有很多坑人的地方，实际应该使用现有的优秀库，比如 moment.js。下面总结一下有可能遇到的坑

### 第一个坑

Date() 返回一个无用的奇怪字符串。比如 `"Fri Apr 03 2015 11:17:29 GMT+0800 (CST)"`。

new Date() 才是返回的 Date 对象

### 第二个坑

d.getDate() 返回的是几号

d.getDay() 返回的是星期几 0~6。礼拜天是 0

### 第三个坑

month 是从 0 开始。

### 第四个坑

toLocalString 不是由 JS 决定的，而是由浏览器或者操作系统决定的，同样的代码放到不同的浏览器或者电脑或者不同的地区，显示的结果完全不一样，完全不可靠，不能用。

### 第五个坑

构造时间对象时候一定要用时间戳（或者 UTC 方法），这样不管在地球上的哪个角落都将会得到一个表示同一时刻的时间对象。比如 `new Date(2000,0,1,0,0,0) ` 这行代码，再不同的地区或国家得到的时间对象所代表的时间是不一样的，所以不能这样用。



每天是 86400 秒，记住这个数字。遇到 BUG 时候也许用得上它。





