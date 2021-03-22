# react

## 最初设想

Dom 操作一般需要经过三个步骤：

1. 从页面中取元素到 JS 中
2. 进行一些操作
3. 将操作后的元素回填到页面中

DOM 操作是很繁琐的，而且 DOM api 又是出了名的难用。React将上面步骤简化。

React 的设想：将上面步骤改成

1. 用 JS 生成一个虚拟的 DOM 对象
2. 将这个虚拟的 DOM 对象填回到页面中

也就是说省去了从页面中获取元素的步骤，只往页面里放东西不取东西。React 就是在这种理念下被创造出来的。

代码及简化历程见 [GitHub](https://github.com/zhangxin/react-demos/blob/master/script.js) 以及 [jsbin](http://js.jirengu.com/yuvuy/1/edit?html,js,output)



特点：页面要留空

虚拟 Dom：虚拟 Dom 就是非真实的 Dom，是一个表示 Dom 节点的对象

JSX：就是用 HTML 的形式写 JS。是一种 JS 的扩展