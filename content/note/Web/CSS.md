---
title: CSS笔记
tags:
  - Note
  - Web
  - CSS
date: 2023-12-23
description: 关于CSS的语法
slug: css-note
---

# 选择器

## 标签选择器

```html
<style>
  div {
    color: lightblue;
  }
</style>
<body>
  <div>11111送地狱火</div>
</body>
```

## 类选择器

```html
<style>
  .classname {
    color: lightblue;
  }
</style>
<body>
  <div class="classname">11111送地狱火</div>
</body>
```

## id 选择器

```html
<style>
  #idname {
    color: lightblue;
  }
</style>
<body>
  <div id="idname">11111送地狱火</div>
</body>
```

- 优先级：id 选择器 > 类选择器 > 标签选择器
  - 使用!important 提高优先级到最前

```html
  <style>
    .classname {
      color: lightblue !important;
    }
  </style>
```

## 后代选择器

选择指定元素的后代元素

```html
<style>
  #paragraph p {
    color: lightskyblue;
  }
</style>
<body>
  <div id="paragraph">
    <p>这是一个段落</p>
  </div>
</body>
```

### 子选择器

选择指定父元素下的直接子元素

```html
<style>
  ul > li{
    color: lightskyblue;
  }
</style>
<body>
  <ul>
    <li>1</li>
    <li>2</li>
  </ul>
</body>
```

### 相邻兄弟选择器

选择紧接在指定元素后的第一个同级元素

```html
<style>
  h1 + p{
    color: lightskyblue;
  }
</style>
<body>
  <h1>嗨嗨嗨</h1>
  <p>我被选上了</p>
  <p>我没被选上</p>
</body>
```

### 通用兄弟选择器

选择指定元素之后的所有同级元素

```html
<style>
  h1 ~ p{
    color: lightskyblue;
  }
</style>
<body>
  <h1>嗨嗨嗨</h1>
  <p>我被选上了</p>
  <p>我也被选上了</p>
</body>
```

### 群组选择器

```html
<style>
  div,
  span {
    color: lightskyblue;
  }
</style>
<body>
  <div>段落一</div>
  <span>段落二</span>
</body>
```

### 属性选择器

通过正则匹配元素

- 选择元素 E，attr 为 E 的属性
- `E[attr^="xx"]`选择 attr 属性是以 xx 开头的任何字符
- `E[attr$="xx"]`选择 attr 属性是以 xx 结尾的任何字符
- `E[attr*="xx"]`选择 attr 属性是包含 xx 的任何字符

```html
<style>
  a[href^="#"] {
    color: rgb(179, 255, 0);
  }
  a[href$="org"] {
    color: rgb(195, 0, 255);
  }
  a[href*="un"] {
    background-color: rgb(0, 255, 149);
    color: white;
  }
</style>
```

### 伪类选择器

- 链接
  - `a:link` 普通的、未被访问的链接
  - `a:hover` 鼠标指针位于链接的上方
  - `a:active` 链接被单击的时刻
  - `a:visited` 用户已访问的链接
  - 对于超链接的伪类，我们推荐的使用顺序是:`:link` =>`:visited`=>`:hover`=>`:active`

```html
<style>
  a:link {
    color: red;
  }
  a:visited {
    color: blue;
  }
  a:hover {
    color: green;
  }
  a:active {
    color: yellow;
  }
</style>
```

- 选择器
  - `E:first-child` 选择第一个子元素
  - `E:last-child` 选择最后一个子元素
  - `E:nth-child(n)` 选择第 n 个子元素，n 有三种取值，数字、odd 和 even 注意第一个子元素的下标是 1
  - `E:only-child` 选择在父元素下有且只有一个元素的子元素
  - `E:first-of-type` 选择父元素下第一个 E 类型的子元素
  - `E:last-of-type` 选择父元素下最后一个 E 类型的子元素
  - `E:nth-of-type(n)` 选择父元素下第 n 个 E 类型的子元素，n 有三种取值，数字、odd 和 even
  - `E:only-of-type` 选择父元素有且只有一个 E 类型的子元素
  - `E:nth-last-child(n)` 选择倒数的第 n 个子元素
  - `E:nth-last-of-type(n)` 选择倒数的第 n 个同类型的子元素

```html
<style>
  div {
    width: 100px;
    height: 100px;
    margin-top: 10px;
    background-color: rgb(0, 255, 242);
  }
  div:nth-child(2) {
    background-color: rgb(0, 255, 128);
  }
  div:nth-of-type(4) {
    background-color: rgb(111, 0, 255);
  }
</style>
```

- UI 伪类选择器
  - `:focus` 给获取焦点的元素设置样式
  - `::selection` 给页面中被选中的文本内容设置样式
  - `:checked` 给被选中的单选框或者复选框设置样式
  - `:enabled` 给可用的表单设置样式
  - `:disabled` 给不可用的表单设置样式
  - `:read-only` 给只读表单设置样式
  - `:read-write` 给可读写的表单元素设置样式
  - `:valid` 验证有效
  - `:invalid` 验证无效

```html
<style>
  /*格式错误*/
  .test1 input:invalid {
    background-color: red;
  }
  /*格式正确*/
  .test1 input:valid {
    background-color: green;
  }
  .test2 input:focus {
    background-color: rgb(255, 153, 0);
  }
</style>
<body>
  <div class="test1">
      电子邮箱：<input type="email" />
  </div>
  <div class="test2">
      姓名：<input type="text" /><br />
      密码：<input type="password" />
  </div>
</body>
```

### 其他选择器

# 背景样式

- `background-color` 给指定标签元素设置背景色
- `background-image` 把图像插入背景
  - url("图片地址")
  - `linear-gradient(to 终点|角度，颜色1, 颜色2...)`线性渐变
  - `radial-gradient(形状, 颜色1, 颜色2...)`径向渐变
    - circle 圆形
    - ellipse 椭圆
  - `repeating-radial-gradient(选项, 颜色1, 颜色2...)`重复性径向渐变
- `background-size` 给背景图设置大小
  - length
  - percentage
  - cover
  - contain
- `background-position` 改变图像在背景中的位置
- `background-repeat` 设置背景图像是否平铺
  - `repeat` 背景图像将在垂直方向和水平方向重复（默认值）
  - `repeat-x` 背景图像将在水平方向重复
  - `repeat-y` 背景图像将在垂直方向重复
  - `no-repeat` 背景图像将仅显示一次

```html
<style>
  body {
    background-color: yellowgreen;
    background-image: url("moon.jpg"),url("moon.jpg");
    background-image: linear-gradient(#ff577f, #c6c9ff);
    background-image: linear-gradient(to bottom right, #8ad7c1, #c6c9ff);
    background-image: linear-gradient(50deg, #bc6ff1, #ffd5cd);
    background-image: radial-gradient(#ff577f, #c6c9ff, #8ad7c1);
    background-image: radial-gradient(#8bcdcd 5%, #ff9d72, #c6c9ff);
    background-image: radial-gradient(ellipse, #8ad7c1, #c6c9ff, #fce2ce);
    background-size: 300px 300px;
    background-position: center, right bottom;
    background-repeat: no-repeat, repeat;
  }
</style>
```

# 字体属性

- `font` 在一个声明中设置所有的字体属性
  - font-style
  - font-variant
  - font-weight
  - font-size（或 line-height）
  - font-family
- `font-family` 设置字体类型
  - 字体名称
  - inherit
- `font-size`设置字体大小
  - xx-small
  - x-small
  - small
  - medium（默认）
  - large
  - x-large
  - xx-large smaller
  - larger length
  - %
  - inherit
- `font-weight`设置字体粗细
  - normal（默认）
  - bold
  - bolder
  - lighter
  - inherit 100、200…900（400=normal，700=bold）
- `font-style`设置字体风格
  - normal
  - italic
  - oblique
  - inherit
- `text-shadow` 文本阴影
  - text-shadow: x-offset y-offset blur color;
- `text-overflow` 设置超长文本省略显示
  - `clip` 修剪文本
  - `ellipsis` 显示省略符号来代表被修剪的文本
  - 需要加上以下属性才可正常使用
    - overflow: hidden;
    - white-space: nowrap;
    - display: block;

```html
<style>
  span {
    font: italic 16px 华文彩云;
    font-family: Arial;
    font-size: xx-small;
    font-weight: 100;
    font-style: italic;
    text-shadow: 1px -2px 1px red
  }
</style>
```

- `line-height` 设置行高
  - normal：取决于用户端
  - number：数字乘以元素的字体大小
  - length：长度值可以是像素（px）、英寸（in）、厘米（cm）等单位
  - %：相对于当前元素的字体大小的百分比

```html
<style>
p {
  /* 浏览器文本大小 */
  line-height: normal;
  /* 字体1.5倍 */
  line-height: 1.5;
  /* 24px高 */
  line-height: 24px;
  /* 字体150% */
  line-height: 150%;
}
</style>
```

- `text-align` 设置文本对齐方式
  - left
  - right
  - center
  - justify
  - start
  - end
- `text-decoration` 设置文本样式
  - `line` 设置线的位置
    - underline 下划线
    - overline 上划线
    - line-through 中划线
  - `color`设置线的颜色
  - `style`设置线的样式
    - wavy 波浪线
    - solid 实线
    - dashed 虚线
  - `thickness`设置线的粗细

```html
<style>
  .cls {
    text-decoration: dashed underline overline lime 5px;
    /*圆点上划线和下划线*/
  }
</style>
```

# 列表样式

- `list-style` 在一个声明中设置所有的列表属性
- `list-style-image`设置图像为列表项标志
  - URL
- `list-style-position`设置列表中列表项标志的位置
  - inside
  - outside
  - inherit
- `list-style-type`设置列表项标志的类型
  - disc(默认)
    - circle(圆圈)
    - square
    - decimal

```html
<style>
  ul {
    list-style-position: inside;
    list-style-image: url(list.gif);
    list-style-type: disc;
    list-style: circle url(list.gif) inside;
  }
</style>
<body>
  <ul>
    <li>喵</li>
    <li>喵</li>
  </ul>
</body>
```

# 盒子模型

盒子模型包括内容(content),内边距(padding),边框(border),外边距(margin),宽和高等属性

## 内边距

- `padding`属性是一个复合属性，代表们盒子模型中的填充，也就是内容区域外的空白区域
- padding: 上 右 下 左;
  - padding-top: 属性值;
  - padding-left: 属性值;
  - padding-right: 属性值;
  - padding-bottom: 属性值;

## 边框

- `border`属性是一个复合属性，代表我盒子模型中的边框
- `border-width`边框宽度，宽度一般数值即可
- `border-style`边框线的样式
  - `solid`实线
  - `dashed`虚线
  - `dotted`点线
  - `double`双线
- `border-color`边框线的颜色
- `border-radius`设置圆角边框
  - border-radius: 上 右 下 左;
    - border-top-left-radius: 属性值;
    - border-top-right-radius: 属性值;
    - border-bottom-right-radius: 属性值;
    - border-bottom-left-radius: 属性值;

border、border-width、border-style、border-color 都是复合属性，我们也可以单独设置某条边框的样式

```html
<style>
  div {
    border: 1px solid red;
    border-top: 2px solid blue;
    border-bottom: 3px solid green;
    border-left: 4px solid yellow;
    border-right: 5px solid pink;
    border-radius: 140px 20px 30px 40px; /*四个圆角直径不同*/
  }
</style>
```

## 外边距

- `margin`属性是一个复合属性
- margin: 上 右 下 左
  - margin-top: 属性值;
  - margin-left: 属性值;
  - margin-right: 属性值;
  - margin-bottom: 属性值;
- margin: 上边距 左右边距 下边距;
- margin: 上下边距 左右边距;

## 盒子阴影

`box-shadow`可以用来设置一个或多个下拉阴影的框，视觉效果就像是盒子有了阴影一样

- box-shadow: h-shadow v-shadow blur spread color inset;
  - `h-shadow` 必选，水平阴影的位置，允许负值
  - `v-shadow` 必选，垂直阴影的位置，允许负值
  - `blur` 可选，模糊距离
  - `spread` 可选，阴影的大小
  - `color` 可选，阴影的颜色
  - `inset` 可选，将外部阴影改为内部阴影

```html

```

# display 布局

- none 隐藏元素
- block 块元素
- inline 行内元素
- inline-block 行内块元素

```html
<style>
  span {
    display: block;
  }
  div {
    display: inline;
  }
  a {
    background-color: rgb(95, 118, 160);
    display: inline-block;
    width: 70px;
    height: 30px;
  }
  p {
    display: none;
  }
</style>
<body>
  <span>蓝桥</span><span>云课</span>
  <div>蓝桥</div>
  <div>云课</div>
  <a href="#"></a>
  <a href="#"></a>
  <p>看不见我</p>
</body>
```

## flex 布局

- flex-direction:指定了弹性子元素在父容器中的排列方向和顺序
  - `row` 横向从左到右排列（左对齐），默认的排列方式
    - `row-reverse` 反转横向排列（右对齐），从后往前排，最后一项排在最前面
    - `column` 纵向排列
    - `column-reverse` 反转纵向排列，从后往前排，最后一项排在最上面
- flex-wrap:属性用于指定弹性盒子的子元素换行方式
  - `nowrap` 默认， 弹性容器为单行该情况下弹性子项可能会溢出容器
  - `wrap`弹性容器为多行该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行
  - `wrap-reverse` 反转 wrap 排列
- align-items:用来设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式
  - `flex-start` 弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界
    - `flex-end` 弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界
    - `center` 弹性盒子元素在该行的侧轴（纵轴）上居中放置
    - `baseline` 如弹性盒子元素的行内轴与侧轴为同一条，则该值与 flex-start 等效其它情况下，该值将参与基线对齐
    - `stretch` 如果指定侧轴大小的属性值为 auto，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照 min/max-width/height 属性的限制
- align-content:用于控制多行的对齐方式，如果只有一行则不会起作用
  - `stretch` 默认各行将会伸展以占用剩余的空间
  - `flex-start` 各行向弹性盒容器的起始位置堆叠
  - `flex-end` 各行向弹性盒容器的结束位置堆叠
  - `center` 各行向弹性盒容器的中间位置堆叠
  - `space-between` 各行在弹性盒容器中平均分布
  - `space-around` 各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半

```html
<style>
  div{
    width: 150px;
    height: 150px;
    border: 1px solid #c3c3c3;
    display: flex;
  }
  .content1 {
    flex-direction: row; /*默认值，行对齐，主轴起点与终点相同*/
  }
  .content2 {
    flex-direction: row-reverse; /*行对齐，主轴起点与终点相反*/
  }
  .content3 {
    flex-direction: column; /*列对齐，主轴起点与终点相同*/
  }
  .content4 {
    flex-direction: column-reverse; /*列对齐，主轴起点与终点相反*/
  }
  .box {
    width: 50px;
    height: 50px;
    color: black;
  }
</style>
<body>
  <div class="content1">
    <div class="box" style="background-color:#FFE5B9;">A</div>
    <div class="box" style="background-color:#EFF8FF;">B</div>
  </div>
  <div class="content2">
  <div class="box" style="background-color:#FFE5B9;">A</div>
  <div class="box" style="background-color:#EFF8FF;">B</div>
  </div>
  <div class="content3">
    <div class="box" style="background-color:#FFE5B9;">A</div>
    <div class="box" style="background-color:#EFF8FF;">B</div>
  </div>
  <div class="content4">
    <div class="box" style="background-color:#FFE5B9;">A</div>
    <div class="box" style="background-color:#EFF8FF;">B</div>
  </div>
</body>
```

```html
<style>
  div {
    width: 100px;
    height: 100px;
    color: black;
  }
  #content {
    width: 240px;
    height: 300px;
    background-color: white;
    display: flex;
    flex-wrap: wrap-reverse;
  }
</style>
<body>
  <div id="content">
      <div style="background-color: #ffe5b9">1</div>
      <div style="background-color: #eff8ff">2</div>
      <div style="background-color: #c9cbff">3</div>
  </div>
</body>
```

```html
<style>
  div {
    width: 100px;
    color: black;
  }
  #content {
    width: 240px;
    height: 300px;
    background-color: white;
    display: flex;
    align-items: stretch;
  }
</style>
<body>
  <div id="content">
    <div style="background-color: #ffe5b9">1</div>
    <div style="background-color: #eff8ff">2</div>
    <div style="background-color: #c9cbff">3</div>
  </div>
</body>
```

```html
<style>
  div {
    width: 60px;
    color: black;
  }
  #content {
    width: 300px;
    height: 300px;
    background-color: antiquewhite;
    display: flex;
    flex-wrap: wrap;
    align-content: stretch;
  }
  .left {
    background-color: gray;
  }
  .center {
    background-color: silver;
  }
  .right {
    background-color: darkgray;
  }
</style>
<body>
  <div id="content">
    <div class="left">div1块</div>
    <div class="center">div2块</div>
    <div class="right">div3块</div>
    <div class="left">div4块</div>
    <div class="center">div5块</div>
    <div class="right">div6块</div>
    <div class="left">div7块</div>
    <div class="center">div8块</div>
    <div class="right">div9块</div>
    <div class="left">div10块</div>
    <div class="center">div11块</div>
    <div class="right">div12块</div>
  </div>
</body>
```

## grid 布局

- grid 将网页划分成一个个网格，可以利用这些网格组合出各种各样的布局
  - `grid-template`：设置网格列数和行数
  - `grid-template-columns`：设置网格列数
    - `repeat()`：重复设置列数
    - 数字 每列大小，每个数字设置一列
    - 百分比
  - `grid-template-rows`：设置网格行数
  - `grid-gap`：设置网格行间距和列间距
  - `grid-column-gap`：设置网格列间距
  - `grid-row-gap`：设置网格行间距
  - `grid-area`: 设置区域重复相同元素
    - 行起始 / 列起始 / 行结束 / 列结束

```html
<style>
  .cls{
    display: grid;
    row-gap: 10px;
    column-gap: 10px;
    grid-template-columns: 45px 75px 45px 45px 45px 75px 45px 45px;
    grid-template-rows: repeat(6, 40px);
  }
  div{
    border: 1px solid black;
  }
  .item{
    grid-area: 1 / 1 / 3 / 4
  }
</style>
<body>
  <div class="cls">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div class="item"></div>
  </div>
</body>
```

## -webkit-box 布局

- `-webkit-box-orient`指定盒子内子元素的排列方向
  - `horizontal`（水平方向）
  - `vertical`（垂直方向）
- `-webkit-box-direction`：指定子元素的排列顺序
  - `normal`（正常顺序）
  - `reverse`（反向顺序）
- `-webkit-box-pack`指定子元素在父容器中的对齐方式（水平方向）
  - `start`（默认，从开头对齐）
  - `end`（从结尾对齐）
  - `center`（居中对齐）
  - `justify`（两端对齐）
  - `flex-start`（从开头对齐，与 `start` 相同）
  - `flex-end`（从结尾对齐，与 `end` 相同）
- `-webkit-box-align`指定子元素在父容器中的对齐方式（垂直方向）
  - `start`（从开头对齐）
  - `end`（从结尾对齐）
  - `center`（居中对齐）
  - `baseline`（基线对齐）
  - `stretch`（默认，拉伸以适应容器高度）
- `-webkit-box-flex`指定子元素在弹性盒子中的扩展比例
  - 数值，默认为 0
- `-webkit-line-clamp` 在限制高度的容器中控制多行文本的显示行数，并在超出指定行数时显示省略号
	- 整数值，表示希望显示的文本行数
	- 与下列属性同时使用才可正常显示
		- `display: -webkit-box`
		- `-webkit-box-orient: vertical; `
		- `overflow: hidden;`

# float 属性

- `float`属性用于设置元素浮动
  - left（左浮动）
  - right（右浮动）

```html
<style>
  img:first-child {
    float: left;
  }
  img:nth-child(2) {
    float: right;
  }
</style>
<section>
  <img src="https://labfile.oss.aliyuncs.com/courses/10532/lotus1.png" />
  <img src="https://labfile.oss.aliyuncs.com/courses/10532/lotus2.png" />
</section>
```

# position 定位

- `position`属性用于设置元素的定位类型
  - static
  - relative（相对定位）
  - absolute（绝对定位）
  - fixed（固定定位）
  - sticky（粘性定位）

## static

该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top, right, bottom, left 和 z-index 属性无效。

## relative

该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）

```html
<style>
  .cls {
    position: relative;
    top: 100px;
    left: 100px;
  }
</style>
```

## absolute

元素会被移出正常文档流，并不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。

```html
<style>
  .cls {
    position: absolute;
    right: 30px;
    top: 150px;
  }
</style>
```

## fixed

元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。fixed 属性会创建新的层叠上下文。当元素祖先的 transform、perspective、filter 或 backdrop-filter 属性非 none 时，容器由视口改为该祖先。

```html
<style>
  .cls {
    position: fixed;
    top: 100px;
    right: 0;
  }
</style>
```

## sticky

粘性定位可以被认为是相对定位和固定定位的混合。元素在跨越特定阈值前为相对定位，之后为固定定位，固定在父容器或视口的某个位置

```html
<style>
  .cls {
    position: sticky;
    top: 0;
  }
</style>
```

# transform 变化

- rotate 旋转
  - rotateX 沿 X 轴旋转
  - rotateY 沿 Y 轴旋转
- translate 平移
  - translateX 沿 X 轴平移
  - translateY 沿 Y 轴平移
- scale 缩放
  - scaleX 沿 X 轴缩放
  - scaleY 沿 Y 轴缩放
- skew 倾斜
  - skewX() 沿着 X 轴方向倾斜元素
  - skewY() 沿着 Y 轴方向倾斜元素

```html
<style>
  .cls {
    transform: rotate(-60deg);
    transform: rotateX(70deg);
    transform: translate(100px);
    transform: translate(100px, 150px);
    transform: translateX(100px);
    transform: scale(2);
    transform: scale(2, 3);
    transform: scaleX(2);
  }
</style>
```

# transition 过渡

过渡可以实现元素从一种样式逐渐改变为另一种的效果

- transition: 指定属性 持续时间 速度曲线 开始时间;
  - transition-property: 属性值
  - transition-duration: 属性值
  - transition-timing-function: 属性值
    - `ease` 慢速开始，然后变快，然后慢速结束的过渡效果(cubic-bezier(0.25,0.1,0.25,1))
    - `linear` 以相同速度开始至结束的过渡效果(cubic-bezier(0,0,1,1))
    - `ease-in` 以慢速开始的过渡效果( cubic-bezier(0.42,0,1,1))
    - `ease-out` 以慢速结束的过渡效果( cubic-bezier(0,0,0.58,1))
    - `ease-in-out` 以慢速开始和结束的过渡效果(cubic-bezier(0.42,0,0.58,1))
    - `steps(int,start|end)`第一个为步长，其值必须为整数
      - start(可选)
      - end(可选)
    - `step-start` 相当于 steps(1, start)
    - `step-end` 相当于 steps(1, end)
    - `cubic-bezier(n,n,n,n)`定义自己的变化值可能的值是 0 至 1 之间的数值
    - `initial` 规定使用默认值
    - `inherit` 规定从父元素继承该属性值
  - transition-delay: 属性值

```html
<style>
  div {
    /*ease-in-out 慢速开始慢速结束*/
    transition: transform 1s ease-in-out;
  }
  div:nth-child(2) {
    transform: rotate(-60deg);
  }
  div:hover {
    transform: scale(2);
  }
</style>
<body>
  <div></div>
  <div></div>
</body>
```

# 动画

## 关键帧

关键帧动画可以定义动画的每一帧的样式，当动画播放的时候，动画会按照关键帧上定义的样式播放

```html
<style>
  @keyframes 动画名{
    0% {样式属性：属性值;}
    25% {样式属性：属性值;}
    50% {样式属性：属性值;}
    100% {样式属性：属性值;}
  }
</style>
```

## 动画

动画需要设置动画的名称，并且需要设置动画的时长

- animation: 动画名 完成动画的周期 是否重复;
  - `animation-name`: 属性名;
  - `animation-duration`: 属性名
    - 规定动画完成一个周期所花费的秒或毫秒默认是 0
  - `animation-timing-function`: 属性名
    - 规定动画的速度曲线默认是 "ease"
  - `animation-fill-mode`: 属性名
    - 规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式
  - `animation-delay`: 属性名
    - 规定动画何时开始默认是 0
  - `animation-iteration-count`: 属性名
    - 规定动画被播放的次数默认是 1
  - `animation-direction`: 属性名
    - 规定动画是否在下一周期逆向地播放默认是 "normal"

```html
<style>
  .cls{
    animation-name: action;
    animation-duration: 9s;
    animation-iteration-count: 10;
  }
  @keyframes action {
    0% {
      margin-left: 400px;
    }
    25% {
      background-color: #dd7631;
    }
    50% {
      border-radius: 10%;
    }
    100% {
      margin: 100px;
    }
  }
</style>
```

# media 查询

- media 属性让浏览器根据不同的媒体条件来应用不同的样式规则
  - mediatype：种类
    - `all` 适用于所有设备
    - `print` 用于打印机和打印预览
    - `screen` 用于电脑屏幕，平板电脑，智能手机等
    - `speech` 用于屏幕阅读器等发声设备
  - media feature: 条件
    - `max-width` 定义输出设备中的页面最大可见区域宽度
    - `max-height` 定义输出设备中的页面最大可见区域高度
    - `min-width` 定义输出设备中的页面最小可见区域宽度
    - `min-height` 定义输出设备中的页面最小可见区域高度
    - `orientation` 视口（viewport）的旋转方向 portrait ：表示 viewport 处于纵向，即高度大于等于宽度 ；landscape：表示 viewport 处于横向，即宽度大于高度

```html
<style>
  /* css样式 */
  @media mediatype and|not|only (media feature) {
      CSS-Code;
  }
  /* 链入外部样式表 */
  <link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystyle.css">
</style>
```
