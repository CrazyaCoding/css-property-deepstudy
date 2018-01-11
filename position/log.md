#position
##概念
    MDN: 用于指定一个元素在文档中的定位方式。top, right, bottom 和 left 属性则决定了该元素的最终位置。
    w3school: 这个属性定义建立元素布局所用的定位机制。任何元素都可以定位，不过绝对或固定元素会生成一个块级框，而不论该元素本身是什么类型。相对定位元素会相对于它在正常流中的默认位置偏移。
##取值
    static: 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
    inherit: 规定应该从父元素继承 position 属性的值。
    relative: 生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。
    absolute: 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
    fixed: 生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
    
##问题
* 设置position属性的top left等属性的百分比是相对于谁的
* 设置为relative元素后，会不会把兄弟元素挤走
* 设置为relative的元素脱离文档流了吗

##解答
* 相对于父元素
* 不会，是在本身的位置去偏移，只会造成重叠，对其他元素不造成影响
* 不脱离 absolute fixed会早成脱离文档流















