# SCSS

## SCSS 是什么

[SCSS](https://zh.wikipedia.org/wiki/Sass)

Sass（英文全称：Syntactically Awesome Stylesheets）。可以看作是加强版的 CSS。

是一个最初由 Hampton Catlin 设计并由 Natalie Weizenbaum 开发的类 CSS 语言。

发行时间：2007年
稳定版本：2016年3月28日

Sass 十分简洁，语法中几乎不含括号。后来很多人表示不含括号看不懂，于是 Sass 的开发者又提供了 Scss，含括号。这些人终于表示能看懂了。

Sass 的官方解释器是开源的并且用 Ruby 语言写成，但是也有用PHP、C 语言、Java 等实现的版本（C语言版本叫做 llibSass，Java 语言版本叫做 JSass）。

SassScript 提供以下功能：变量、嵌套、混入（Mixin）、选择器继承等。

SCSS 的历史

Ruby 社区有一个全栈框架叫做 Rails，很多 Ruby 程序员在写前端时候发现 HTML CSS JS 都不好用，于是 Ruby 社区发明了新的语法，分别是 HAML，SCSS->SASS，coffeeScript。这些语言有的已经不再使用（比如 coffeeScript），但是也影响了前端的发展。比如在 node 社区使用 node 实现了 SASS，coffeeScript 影响了 ES6 和 Typescript 的发展。

1. 安装与运行
   1. 零配置学习 - 使用 parcel
   2. 零配置学习 - 使用 jsbin.com
2. 最简单的几个语法
   1. 嵌套选择器
   2. 变量
   3. mixin
   4. placeholder

### BEM 命名法