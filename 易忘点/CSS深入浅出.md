## 1.css不正交
- position: fixed VS transform
  - 父元素设置了transform属性以后，会让子元素的`position:fixed`效果消失，变的和`position:absolute`一样。
- margin VS border
- 小圆点 VS display
- position: absolute VS display: inline
  - 设置了`position: absolute`后，会让`display: inline 或 inline-block`的元素变为`display:block`。
 ## 2. 宽度与高度
  - 设计师在设计字体时候会给一个建议行高，包裹内联元素的块级元素的高度就是内联元素的行高。
  - 两个inline或者inline-block元素之间有任何的分隔，比如换行、tab、空格，他们之间都会显示一个且只有一个空格
  - 文字两端对齐的套路
    - [套路](http://js.jirengu.com/yimiz/1/edit?html,output)
  - word-break  
    - 控制单词分行
  - white-space
    - 控制不分行，用来处理文本溢出（用省略号代替溢出）
      - 单行文本溢出
      ```
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      ```
  - 文字垂直居中
    - 高度要自适应，利用padding让元素居中，不要固定高度
  - div高度的确定
    - div的高度是由其内部文档流中块级元素和内联元素(即行高line-height)的高度和确定的。
    - 脱离文档流的意思是父元素在算高度时候不算上它，就像它不存在一样。

 ## 3.堆叠上下文