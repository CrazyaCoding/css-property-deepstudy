#概念
    MDN  
    一个块格式化上下文（block formatting context）是Web页面的可视化CSS渲染出的一部分。它是块级盒布局出现的区域，也是浮动层元素进行交互的区域。
    W3C
    BFC (Block Formattng Context)块圾格式上下文，是web页面中盒模型布局的css渲染模式，它的定位体系属于常规文档流。

一个块格式化上下文由以下之一创建：
    
    * 根元素或其它包含它的元素
    * 浮动元素 (元素的 float 不是 none)
    * 绝对定位元素 (元素的 position 为 absolute 或 fixed)
    * 内联块 (元素具有 display: inline-block)
    * 表格单元格 (元素具有 display: table-cell，HTML表格单元格默认属性)
    * 表格标题 (元素具有 display: table-caption, HTML表格标题默认属性)
    * 具有overflow 且值不是 visible 的块元素，
    * display: flow-root
    * column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被包裹在一个多列容器中。

一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。

块格式化上下文对于定位 (参见 float) 与清除浮动 (参见 clear) 很重要。定位和清除浮动的样式规则只适用于处于同一块格式化上下文内的元素。浮动不会影响其它块格式化上下文中元素的布局，并且清除浮动只能清除同一块格式化上下文中在它前面的元素的浮动。

#如何形成的
    浮动，绝对定位元素，inline-blocks,table-cells,table-captions,和overflow的值不为visible的元素，（除了这个值已经被传到了视口的时候）将创建一个新的块级格式化上下文。
    举例说明能够生成一个新的BFC的例子：
    float的值不为none
    position的值不为relative或者static
    display的值为table-cell table-caption inline-block flex 或者inline-flex中的一个
    overflow不为visible
    
#BFC导致的外边距重叠
```
//见index.html
<div class="box">
        <p>盒子1</p>
        <p>盒子2</p>
        <p>盒子3</p>
</div>

<style>
    .box{
        overflow: hidden; /*仅仅用作形成一个BFC*/
        background: rebeccapurple;
    }
    .box p{
        margin:10px 0;
        background: salmon;
        width: 300px;
        height: 200px;
    }
</style>

// 结果就是两个子div之间的间距变成 10px 而不是叠加的20px 被成为外边距重叠
// 这样的情况仅仅发生在两个相邻的块级盒子在同一个BFC中才会发生，所以如果处于不同的BFC就不会发生外边距重叠
// 所以，解决办法就是制造一个新的BFC块

<div class="box">
    <p>p1</p>
    <p>p2</p>
    <div class="bfc2">
        <p>p3</p>
    </div>
</div>

.bfc2{
    overflow: hidden;
}

// 结果就是p3 与p2之间的距离变为20px
```
#为了清除浮动创建的BFC
    通常情况下，容器内部含有浮动元素，导致容器没有高度变成塌陷了
    可以通过创建一个BFC来解决这个问题，计算BFC高度的时候，浮动元素的高度也计算在内
    
#使用BFC来阻止文字环绕
    原理是BFC的元素的左边总是与包含快的左边相接触
    见index3.html
    给p标签增加overflow: hidden 创建一个新的BFC，生成新的包含快，BFC的定义是左边与包含快的左边紧紧相接触，所以文字环绕现象消除
    
#参考
[MDN-BFC](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
[BFC](https://www.w3cplus.com/css/understanding-block-formatting-contexts-in-css.html)