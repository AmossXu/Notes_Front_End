### CSS 权重问题

1. ！important
2. 内联样式 如style = ""
3. ID选择器
4. 类，伪类和属性选择器
5. 标签选择器和为元素选择器如 div p

### 盒子模型
- 标准盒模型：盒子是a*b box-sizing:content-box
- 诡异盒模型: 所有是a*b box-sizing:border-box

### CSS reset 用于改写默认样式

### margin 合并和塌陷问题
- 块级元素的上边距和下边距有时会合并为一个外边距，其大小取其中的最大者，这种行为称为外边距合并
解决：
    1. 使用padding
    2. 设置定位或者浮动 内层元素绝对定位position:absolute 或者 float
    3. 改变盒子模型 display：inline-block;
 - margin 塌陷 两个块内嵌其中内部margin top50  外面的也会有
 解决：
    1. 父元素设置 overflow: hidden;

### 居中
- 文本居中 父元素：text-align:center
- div居中 水平居中 自身：margin:0 auto;
    -垂直居中： 
```css
#div1{
    width:200px;
    height:200px;
    position:absolute;
    left:50%;top50%;//定位点在左上角所以要回到中间
    margin-left：-100px;
    margin-top:-100px;
}
```


### 浮动 float
作用：
1. 实现排版布局
2. 所有元素都支持宽高
3. 行内元素会支持宽高

特点
1. 脱离文档流
2. 浮动有方向
3. 块元素宽度尽可能的窄
4. 行内元素会变成块元素
5. 宽度不够会掉下来