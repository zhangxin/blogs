# icon 的各种实现方式

## image

步骤：

1.  设置 img 的大小。
2. 设置 img 的 vertical-align，到合适的位置。

但是该方法存在一个问题：请求过多。

请求是邪恶的吗？服务器的存在就是为了接收请求，所以请求是没有问题的，必要的请求是不可或缺的。有问题的是，明明可以发更少的请求，却发了很多多余的请求，这才是邪恶的。

请求过多有什么影响？要从三个方面来分析：

1. 对于客户端来说，有一个慢的体验，因为每个请求都是要耗费时间建立的。HTTP1.1 时代请求过多客户端会变慢。但是随着 HTTP2 的出现，客户端这边就不慢了，100 个请求跟 1 个是差不了多少的。

2. 对于服务器来说，请求多的话服务器的压力就大。比如，如果后端是用 Java 或者 PHP 实现的，一个请求就可能搞一个线程，请求多的话就要进行线程优化等，服务器压力自然大。
3. 请求过多网站就会消耗更多的流量，减少请求就能减少成本。

## CSS Sprites

正确的名字是 CSS 精灵图，Sprites 是来自于游戏开发的一个术语。雪碧图纯粹是文盲的叫法。

精灵图的基本原理是，把多个图片合成一张大图，然后通过调整 background-position，在不同窗口露出相应的图标。使用 CSS Sprites 可以减少网络请求，提高网页加载性能。比如说一个网站上面有很多图标，当使用背景图片展示这些图标，即 icon 的时候，每个小图标都是一个图片，都对应着一个网络请求，即使是很小的图片。而网络请求本身是有时间开销的，所以应该减少不必要的网络请求，可以把很多的小图片合成一张大图片，在使用的时候做适当的偏移，让窗口中露出合适的图标。

### 合成精灵图的几种方法

1. 纯手工 Photoshop 合成  // 太古老 已经不用
2. 命令行：`sprity create [输出目录] [资源目录] -s [css目录]`  // 需要安装 搜索 npm css sprites 根据项目提示来做
3. 在线工具：`https://spritegen.website-performance.org/`

优点：解决了请求过多的问题

缺点：

1. 没有办法缩放，牵一发而动全身，缩放有可能影响其他图标的正常
2. 不好修改。当需要添加、修改或者删除一个图标时候，要重新从头开始生成一个精灵图。

## Icon Font

Icon Font 的基本原理是将 Icon 定义为字体图标，在 CSS 中用 `@font-face`  引入 Icon Font 自定义字体，再利用 `font-family` 和字符码显示出指定的图标。Icon Font 的实质就是把字体做成图标。一般需要以下步骤：

1. 制作字体文件（利用 iconfont）
2. 声明 font-family
   1. 使用本地链接
   2. 使用第三方链接
3. 使用 font-family
   1. 使用 HTML 实体
   2. 使用CSS `:before` 插入

HTML 实体就是 HTML 中的一些转义字符，以 `&` 开头。一般是 HTML 中的预留字符，比如`<>`必须被替换为字符实体。有两种形式：

1. `&entity_name`
2. `&#entity_number`   // number 是 unicode 码，所有字符都可以用这种形式表示，比如 &#0031 代表数字 1

CSS 不支持使用 HTML 实体。用 CSS 表示 Unicode 字符的方式很简单，即 `\unicode_number`

由于使用的是字体, 因此可以通过 `color`，`font-size` 设置 icon 的样式。Icon Font 拥有比 CSS Sprite 图片更小的文件体积，维护也比图片更方便，但是 Icon Font 通常只能使用单一的颜色，字体文件生成也比 CSS Sprites 更复杂。

## CSS Icon

直接使用 CSS 画出需要的图标

[CSS Icon](https://cssicon.space/#/)

## SVG

SVG 有两种使用方式：

1. img src=svg。即直接把 svg 图片直接插入到页面。这跟最上面的 image 方法没有区别，请求还是很多

2. SVG "sprites" 以标签的形式组织所有图片，移动端项目首选


思路跟上面的 CSS sprites 一样，也是要把两个 svg 合成一个 svg，然后根据需求选择

步骤：

1. 搜索 ”npm svg sprite“
2. 根据提示 安装并使用命令行，生成 symbol
   1. 上面两步也可以使用阿里 iconfont，引入 symbol 即可
3. 引入。可以直接粘贴 `<svg>` 标签声明的 icon，也可以引入外部链接
4. 使用 `<svg>` 标签引入 icon。代码结构一般如下

```html
<svg>
  <use x-link:href="#xxx"></use>
</svg>
```

好处：

1. icon 的颜色可以随意设置
2. icon 可以随意缩放，没有锯齿和失真
3. 添加或者删除 icon 非常方便，这点相对 css sprite 来说优势巨大

## 一些资源

1. 图片合并可以使用这个线上地址 [csssprites.com296](http://csssprites.com/)
2. 在生产环境中使用的图片都需要经过压缩再使用，线上压缩图片地址 [tinypng.com206](https://tinypng.com/)