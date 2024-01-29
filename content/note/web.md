---
title: "Web笔记"
tags: [ "Web" , "Note" , "HTML5" , "CSS" , "JavaScript" ]
date: 2023-12-23
description: "含有Web三件套（HTML5, CSS, JavaScript）的语法"
slug: "web-note"
---

# 信息文件head

```html
<title> 定义页面标题内容
<meta> 有关文档本身的元信息，例如：文档的作者，用于查询的关键词，关于文档的描述等
<style> 定义CSS层叠样式表的内容
<link> 定义外部文件的链接，最常见的用途是链接外部样式表
<script> 定义页面中程序脚本的内容
```

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="path/to/your/style.css">
</head>
```

其中，`name`、`content` 被称为属性，`viewport` 和 `width=device-width`, `initial-scale=1.0` 被称为属性值

添加一个作者的信息和字符编码
```html
<meta name="author" content="Lee,1234567@qq.com" />
<meta charset="utf-8" />
```

# 内容主体body

## 元素类型
### 行级元素
行级元素不会独占一行，只占据它对应标签的边框所包含的空间
- `<span>`: 用于对文本进行分组，是最通用的行内元素。
- `<a>`: 表示超链接。
- `<strong>`, `<em>`: 分别表示强调文本的重要性和斜体文本。
- `<img>`: 表示图像。
- `<br>`: 表示换行。
- `<input>`: 表示输入框。
- `<button>`: 表示按钮。
- `<label>`: 用于标记表单元素。
### 块级元素
块级元素会独占一行，会完全占满父元素的内容区域
- `<div>`: 用于定义文档中的分区或节，是最通用的块级元素。
- `<p>`: 表示段落。
- `<h1>, <h2>, ..., <h6>`: 表示标题，依次为从大到小的标题。
- `<ul>, <ol>, <li>:` 表示无序列表和有序列表。
- `<table>`: 表示表格。
- `<form>`: 表示表单。
- `<header>`, `<footer>`, `<nav>`, `<article>`: HTML5 中的语义块级元素，用于定义页面结构。
- `<section>`, `<aside>`, `<main>`: HTML5 中的语义块级元素，用于更具体的页面结构。

## 标题
```html
<h1>This is a heading</h1>
<h2>This is a heading</h2>
```

## 段落
```html
<p>This is a paragraph.</p>
```

## 链接
```html
<a href="http://www.w3school.com.cn">This is a link</a>
<a href="mailto:123@163.com">邮箱跳转</a>
<a href="tel:123456789">电话跳转</a>
<a name="label">定义标签</a>
<a href="#label">跳转标签</a>
<a href="https://www.baidu.com" target="_blank">在新窗口中打开被链接文档</a>
<a href="https://www.baidu.com" target="_self">在相同的框架中打开被链接文档</a>
<a href="https://www.baidu.com" target="_top">在整个窗口中打开被链接文档</a>
<a href="https://www.baidu.com" target="_parent">在父框架集中打开被链接文档</a>
```

## span盒子
在同一行里放多个span盒子
```html
<span style="color: chocolate; background-color: bisque;">This is a span</span>
```

## 强调
```html
<strong>加粗强调</strong>
```

## 图像
```html
<img src="image.jpg" alt="图像描述" width="12" height="10"/>
```

## div盒子
每个盒子独占一行
```html
<div style="color: chocolate; background-color: bisque;">This is a div</div>
```

## 列表
- type属性修改列表的样式
  - 1 数字
  - a 小写字母
  - A 大写字母
  - i 小写罗马数字
  - I 大写罗马数字
- start属性修改起始号

```html
<ol>
    <li>有序列表</li>
    <li>有序列表</li>
    <li>有序列表</li>
</ol>
```


- type属性修改列表的样式
  - disc 实心圆点
  - circle 空心圆点
  - square 实心方块
```html
<ul>
    <li>无序列表</li>
    <li>无序列表</li>
    <li>无序列表</li>
</ul>
```

```html
<dl>
    <dt>自定义列表</dt>
    <dd>列表的描述</dd>
    <dt>自定义列表</dt>
    <dd>列表的描述</dd>
</dl>
```

## 表格
```html
<table border="1">
    <!-- 边界 -->
    <!-- 标题 -->
    <caption>表格标题</caption>
    <!-- 表头 -->
    <thead>
      <th>表头1</th>
      <th>表头2</th>
      <th>表头3</th>
    </thead>
    <!-- 行 -->
    <tr>
      <!-- 列 -->
      <td>第一行，第一列</td>
      <td>第一行，第二列</td>
      <td>第一行，第三列</td>
    </tr>
    <tr>
      <td>第二行，第一列</td>
      <td>第二行，第二列</td>
      <td>第二行，第三列</td>
    </tr>
    <tr>
      <!-- 跨越上下两行 -->
      <th rowspan="2">21</th>
      <td>22</td>
      <td>23</td>
    </tr>
    <tr>
      <!-- 跨越左右两列 -->
      <td colspan="2">3</td>
    </tr>
</table>
```

## 表单
- 表单用于向服务器传输数据
  - action 提交地址
  - method 提交方式
  - autocomplete 自动填充

```html
<form action="http://www.biadu.com" method="get" autocomplete="on">

</form>
```

### 表单项
#### input标签
##### type属性
- text 文本框
- password 密码框
  - placeholder 提示文本
- radio 单选框
- checkbox 复选框
  - value 值
  - checked 默认勾选
- file 文件上传
  - accept 限制上传的文件类型
- reset 重置按钮
- submit 提交按钮
  - value 按钮的名称
- email 邮箱输入框
- url 网址输入框
- number 数字输入框
  - min 最小值
  - max 最大值
  - step 步长
  - value 默认值
- range 范围输入框
  - min 最小值
  - max 最大值
  - step 步长
  - value 默认值
- date 日期输入框
- datetime-local 日期时间输入框
- search 搜索框
- color 颜色选择框
- form 表单

##### 其他属性
- autofocus 自动获得焦点
- placeholder 提示文本

```html
<form>
  文本框：<input type="text" name="text" placeholder="请输入文本"><br>
  密码：<input type="password" name="password" placeholder="请输入密码"><br>
  单选框：
  <!-- name相同的为相同的选项组 -->
  <input type="radio" name="sex" value="男" checked>男
  <input type="radio" name="sex" value="女">女
        <!-- 空格 -->
     &nbsp;
  <!-- 换行 -->
  <br>
  多选框：
        <input type="checkbox" name="hobby" value="唱">唱
        <input type="checkbox" name="hobby" value="跳">跳
        <input type="checkbox" name="hobby" value="rap">rap
        <input type="checkbox" name="hobby" value="篮球">篮球
  文件选择:<input type="file" name="file"><br>
  email:<input type="email" name="email" placeholder="请输入邮箱"><br>
  url:<input type="url" name="url" placeholder="请输入网址"><br>
  数字:<input type="number" name="number" min="0" max="100" step="2" value="5"><br>
  滑动条:<input type="range" name="range" min="0" max="100" step="2" value="5"><br>
  日期选择:<input type="date" name="date" placeholder="请输入日期"><br>
  日期时间选择:<input type="datetime-local" name="datetime-local" placeholder="请输入日期"><br>
  搜索框:<input type="search" name="search" placeholder="请输入搜索"><br>
  颜色选择:<input type="color" name="color" placeholder="请输入颜色"><br>
  <input type="submit" value="确定">
  <input type="reset" value="重置">
</form>
<form id="form1" action="#" method="get"></form>
<form id="form2" action="#" method="get"></form>
<input type="text" form="form1">
<input type="button" value="form1" form="form1">
<input type="text" form="form2">
<input type="button" value="form2" form="form2">
<input type="text" autofocus placeholder="搜索">
```
#### select 下拉列表
- size 选项的显示数量
- multiple 是否支持多选
```html
<form>
  下拉列表：
 <select name="se1" size="3" multiple>
  <option value="1">选项1</option>
  <option value="2">选项2</option>
  <option value="3">选项3</option>
  <option value="4">选项4</option>
 </select>
</form>
```
#### textarea 文本域
- cols 列数
- rows 行数
```html
<form>
  文本域：
  <textarea name="area1" cols="30" rows="10">hello，world</textarea>
</form>
```

## 语义化标签
- header 标签是头部区域
- nav 标签是导航区域
- article 标签是内容区域
- section 标签是文档中部分内容区域
- aside 标签是侧边内容栏区域
- footer 标签是底部信息区域

## audio音频标签
- controls用于提供播放、暂停和音量控件
- autoplay自动播放
- loop循环播放

```html
<audio src="./music.mp3" controls="controls" autoplay="autoplay" loop="loop"></audio>
```

- source标签
可设置多个数据源
```html
<audio>
  <source src="./music.mp3" type="audio/mp3">
  <source src="./music.ogg" type="audio/ogg">
</audio>
```

## video视频标签
- muted 静音
- poster 封面
```html
<video controls muted poster="./poster.jpg">
  <source src="./video.mp4" />
</video>
```



# CSS
## 选择器
#### 标签选择器
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
#### 类选择器
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
#### id 选择器
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
  - 使用!important提高优先级到最前
```html
  <style>
    .classname {
      color: lightblue !important;
    }
  </style>
```

#### 后代选择器
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

#### 子选择器
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

#### 相邻兄弟选择器
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

#### 通用兄弟选择器
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

#### 群组选择器
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

#### 属性选择器
通过正则匹配元素
- 选择元素E，attr为E的属性
- `E[attr^=“xx”]`选择attr属性是以xx开头的任何字符
- `E[attr^=“xx”]`选择attr属性是以xx结尾的任何字符
- `E[attr^=“xx”]`选择attr属性是包含xx的任何字符
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

#### 伪类选择器
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
  - `E:nth-child(n)` 选择第n个子元素，n有三种取值，数字、odd和even注意第一个子元素的下标是1
  - `E:only-child` 选择在父元素下有且只有一个元素的子元素
  - `E:first-of-type` 选择父元素下第一个E类型的子元素
  - `E:last-of-type` 选择父元素下最后一个E类型的子元素
  - `E:nth-of-type(n)` 选择父元素下第n个E类型的子元素，n有三种取值，数字、odd和even
  - `E:only-of-type` 选择父元素有且只有一个E类型的子元素
  - `E:nth-last-child(n)` 选择倒数的第n个子元素
  - `E:nth-last-of-type(n)` 选择倒数的第n个同类型的子元素
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

#### 其他选择器



## 背景样式
- `background-color` 给指定标签元素设置背景色
- `background-image` 把图像插入背景
  - url("图片地址")
  - `linear-gradient(to 终点|角度，颜色1, 颜色2...)`线性渐变
  - `radial-gradient(形状, 颜色1, 颜色2...)`径向渐变
    - circle圆形
    - ellipse椭圆
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


## 字体属性
- `font` 在一个声明中设置所有的字体属性
  - font-style
  - font-variant
  - font-weight
  - font-size（或line-height）
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
  - 需要加上正常使用
    - overflow: hidden;
    - white-space: nowrap;

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

## 列表样式
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

## 盒子模型
盒子模型包括内容(content),内边距(padding),边框(border),外边距(margin),宽和高等属性

### 内边距
- `padding`属性是一个复合属性，代表们盒子模型中的填充，也就是内容区域外的空白区域
- padding: 上 右 下 左;
  - padding-top: 属性值;
  - padding-left: 属性值;
  - padding-right: 属性值;
  - padding-bottom: 属性值;

### 边框
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

### 外边距
- `margin`属性是一个复合属性
- margin: 上 右 下 左
  - margin-top: 属性值;
  - margin-left: 属性值;
  - margin-right: 属性值;
  - margin-bottom: 属性值;
- margin: 上边距 左右边距 下边距;
- margin: 上下边距 左右边距;

### 盒子阴影
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

## display布局
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
### flex布局
  - flex-direction:指定了弹性子元素在父容器中的排列方向和顺序
    - `row` 横向从左到右排列（左对齐），默认的排列方式
    - `row-reverse` 反转横向排列（右对齐），从后往前排，最后一项排在最前面
    - `column` 纵向排列
    - `column-reverse` 反转纵向排列，从后往前排，最后一项排在最上面
  - flex-wrap:属性用于指定弹性盒子的子元素换行方式
    - `nowrap` 默认， 弹性容器为单行该情况下弹性子项可能会溢出容器
    - `wrap`弹性容器为多行该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行
    - `wrap-reverse` 反转wrap排列
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

### grid布局
- grid将网页划分成一个个网格，可以利用这些网格组合出各种各样的布局
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


## float
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

## position定位
  - `position`属性用于设置元素的定位类型
    - relative（相对定位）
    - absolute（绝对定位）
    - fixed（固定定位）
    - inherit（静态定位）
    - sticky（粘性定位）

### fixed固定定位
相对于浏览器窗口进行定位
```html
<style>
  .cls {
    position: fixed;
    top: 100px;
    right: 0;
  }
</style>
```

### relative相对定位
相对于其正常位置进行定位
```html
<style>
  .cls {
    position: relative;
    top: 100px;
    left: 100px;
  }
</style>
```

### absolute绝对定位
把元素精确地放在任意位置
```html
<style>
  .cls {
    position: absolute;
    right: 30px;
    top: 150px;
  }
</style>
```

### sticky粘性定位
在用户滚动页面时，元素在跨越特定阈值之前是相对定位的，一旦到达阈值，它就会变为固定定位，固定在父容器或视口的某个位置
```html
<style>
  .cls {
    position: sticky;
    top: 0;
  }
</style>
```

## transform变化
- rotate旋转
  - rotateX沿X轴旋转
  - rotateY沿Y轴旋转
- translate平移
  - translateX沿X轴平移
  - translateY沿Y轴平移
- scale缩放
  - scaleX沿X轴缩放
  - scaleY沿Y轴缩放
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

## transition过渡
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
    - `step-start` 相当于steps(1, start)
    - `step-end` 相当于 steps(1, end)
    - `cubic-bezier(n,n,n,n)`定义自己的变化值可能的值是0至1之间的数值
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

## 动画
### 关键帧
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

### 动画
动画需要设置动画的名称，并且需要设置动画的时长
- animation: 动画名 完成动画的周期 是否重复;
  - `animation-name`: 属性名;
  - `animation-duration`: 属性名
    - 规定动画完成一个周期所花费的秒或毫秒默认是0
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

## media查询
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
    - `orientation` 视口（viewport）的旋转方向portrait ：表示viewport处于纵向，即高度大于等于宽度 ；landscape：表示viewport处于横向，即宽度大于高度
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


# JavaScript

## 属性
- classList: 用于获取或修改元素的类列表。
  - 使用 add, remove 添加删除类名，使用 contains 检查是否包含某个类名，使用 toggle 切换类名。
- id: 元素的唯一标识符。
- style: 元素的内联样式属性。
- src: 表示元素的来源，通常用于图像、音频和视频等媒体元素。
- alt: 用于描述图像内容的替代文本，通常在图像无法加载时显示。
- href: 表示链接的目标 URL，通常用于锚点（`<a>` 元素）和链接元素（`<link>`）。
- value: 用于表单元素，表示用户输入或选择的值。
- innerHTML: 元素的 HTML 内容，可以用于读取或写入元素的内容。
- textContent: 元素的文本内容，不包括 HTML 标记，可以用于读取或写入元素的文本。
- disabled: 用于禁用表单元素或按钮。
- checked: 用于表示复选框或单选按钮是否被选中。
- placeholder: 表单元素的占位符文本，通常在输入框中用于提供示例或说明。
- width 和 height: 图像和表格等元素的宽度和高度。
- type: 用于表单元素，表示输入框的类型（文本、密码、按钮等）。
- min 和 max: 用于 `<input type="number">` 等元素，表示允许的最小和最大值。

## 本地存储
- `localStorage` 永久存储
- `sessionStorage` 仅在当前会话下有效
  - `setItem(key,value)` 保存数据到本地存储
  - `getItem(key)` 从本地存储获取数据
  - `removeItem(key)` 根据指定key从本地存储中移除数据
  - `clear()` 清除所有保存数据
- `localstorage`与`cookie`的区别：
  -localStorage解决了早期使用cookie存储遇到的存储空间不足的问题( 每条cookie的存储空间为4k)；
  -localStorage一般浏览器支持的是5M大小，具体存储大小根据浏览器的不同会有所不同
  - 并且相较于cookie而言，localStorage 中的信息不会被传输到服务器
- 那么`localStorage`和`sessionStorage`区别
  - `localStorage` 的生命周期是永久的，除非用户清除localStorage信息，否则这些信息将永远存在
  - `sessionStorage` 的生命周期是临时的，一旦当前窗口或标签页被关闭了，那么通过它存储的数据也就被清空了
```html
<script>
  // 语句 1： 保存数据到本地存储
  localStorage.setItem("ExpireTime", "1527592757");
  localStorage.UserId = "2021008";
  // 语句 2： 根据指定名称获取本地存储中的数据
  var expireTime = localStorage.getItem("ExpireTime");
  console.log(expireTime);
  // 语句 3： 根据指定名称从本地存储中移除
  localStorage.removeItem("ExpireTime");
  // 语句 4： 清除本地存储中所有数据
  localStorage.clear();
</script>
```
```html
<script>
  // 语句 1： 保存数据到本地存储
  sessionStorage.setItem("ShopId", "SH1290333211");
  sessionStorage.ShopNumber = "10";
  // 语句 2： 根据指定名称获取本地存储中的数据
  var ShopId = sessionStorage.getItem("ShopId");
  console.log(ShopId);
  // 语句 3： 根据指定名称从本地存储中移除
  sessionStorage.removeItem("ShopId");
  // 语句 4： 清除本地存储中所有数据
  sessionStorage.clear();
</script>
```


## 运算符
- `===`左右两边的操作数相等且类型相同时，返回 true
- `!==`左右两边的操作数不相等或者类型不相同时，返回 true

## 循环
- `for`遍历
  - `for(i in arr){}`等效于`for(var i = 0; i < arr.length; i++){}`

## 函数
```js
function 函数名(参数){
  ...
  return 返回值;
}
```
### 链式调用
如果返回值为一个函数，则可以继续通过括号当作函数传参调用
```js
function f(...args){
  return (...arg1) => arg1.length ? f(args, arg1) : `参数：${args.join(',')}`;
}

f(param1)(param2)(param3)();
```

## 数组
- `var 数组名 = new Array(元素1, 元素2,...,元素n);`
- `var 数组名 = [元素1, 元素2,...,元素n];`
- 数组切分
  - `var arr2 = arr1.slice(start,end);`
- `arr.unshift(元素)`数组前添加元素
- `arr.shift()`数组前删除元素
- `arr.sort(function(a,b){return a-b})` 排序
- `arr.reverse()`倒序数组
- `arr.join("分隔符")`元素拼接
- `arr1.concat(arr2)`数组拼接
- `arr.includes(元素)`元素判断
- `arr.toString()`值转换成字符串
- `arr.indexOf(元素)`查找下标
- `arr.reducer(function(acc, e){return acc}, init)` 逐个遍历数组元素，将每个元素都经过该函数处理，最后返回单个返回值。其内部函数的返回值将作为下一次调用该函数时的 acc 参数，init 为 acc 的初始值

## 字符串String
- `str.length`获取长度
- `str.toLowerCase()`大写转小写
- `str.toUpperCase()`小写转大写
- `str.charAt(index);`获取指定下标的字符
- `str.substring(start,end);`获取指定下标区间内的字符
- `str.replace(oldstr,newstr);`替换部分字符串
  - `oldstr`部分可使用正则表达
  - `str.replace(regex, (match, offset) => {return newstr});`获取偏移量和自定义替换结果
- `str.split("分隔符");`分割字符串成数组
- `str.indexOf(str);`查找str首次出现的下标

## 库
### Math
- `Math.E` 自然对数的底数
- `Math.LN2` 2的自然对数
- `Math.PI` 圆周率
- `Math.SQRT2` 2的平方根
- `Math.abs(x)` 返回一个数的绝对值
- `Math.pow(x,y)` 返回一个数的y次幂
- `Math.random()` 返回一个0到1之间的伪随机数
- `Math.sqrt(x)` 返回一个数的平方根
- `Math.round()` 返回四舍五入后的整数
- `Math.exp(x)` 返回欧拉常数的参数次方

### Date
- `Date.now()` 返回当前时间戳
- `Date.getDate()` 返回一个月的某一天
- `Date.getDay()` 返回一周中的某一天
- `Date.getFullYear()` 返回年份
- `Date.getHours()` 返回小时
- `Date.getMonth()` 返回月份(0~11)
- `Date.getTime()` 返回毫秒数
- `Date.setFullYear()` 设置年份
- `Date.setDate()` 设置一个月中的某一天
- `Date.setMonth()` 设置月份

## BOM(Browser Object Model)
是浏览器对象模型，通过操作对象的属性和方法来实现与浏览器的交互
- BOM组成
  - document 是 DOM 对象。
  - location 是用于获取或设置窗体。
  - navigation 包含浏览器配置相关的信息。
  - history 浏览器的历史记录。
  - screen 用于显示设备信息。
- 方法
  - `alert()`	显示一个警告框。
  - `prompt()`	显示可提示用户输入的对话框。
  - `confirm()`	显示一个有确认和取消按钮的对话框。
  - `open()`	打开一个新的浏览器页面。
  - `close()`	关闭浏览器页面。
  - `print()`	打印当前窗口内容。
```html
<script>
  function fun(){
    alert("警告框");
    prompt("输入框");
    confirm("有确认和取消的对话框");
    open();
    print();
    close();
  }
</script>
<body>
  <button onclick="fun()">click</button>
</body>
```

## DOM(Document Object Model)
它是浏览器为每个窗口内的HTML页面创建的一个document对象，用来对页面的元素进行操作
- `document.title` 获取文档的title元素
- `document.body` 获取文档的body元素
- `document.URL` 获取文档的 URL
- `document.forms` 获取文档的form元素
- `document.images` 获取文档的img元素
- `document.links` 获取文档的a元素
- `document.cookie` 获取文档的 cookie
- `document.referrer` 返回来用户当前浏览页面的 URL
- `document.getElementById()` 通过id获取元素
- `document.getElementsByClassName()` 通过class获取元素
- `document.getElementsByName()` 通过name获取元素
- `document.getElementsByTagName()` 获取标签的元素
- `document.querySelector()` 通过选择器获取第一个元素
- `document.querySelectorAll()` 通过选择器获取所有元素
- `document.createElement()` 创建元素节点
- `document.createTextNode()` 创建文本节点
- `document.write()` 输出内容
- `document.writeln()` 输出内容并换行
```html
<script>
  function fun(){
    document.writeln(document.title);
    document.writeln(document.body);
    document.writeln(document.URL);
    document.writeln(document.forms);
    document.writeln(document.images);
    document.writeln(document.links);
    document.writeln(document.cookie);
    document.writeln(document.referrer);
    document.writeln(document.getElementById("id"));
    document.writeln(document.getElementsByClassName("className"));
    document.writeln(document.getElementsByName("name"));
    document.writeln(document.getElementsByTagName("div"));
    document.writeln(document.querySelector("#id"));
    document.writeln(document.querySelectorAll("id"));
    document.writeln("writeln");
    document.write("write");
    //write会重写页面
    var button = document.createElement("button");
    button.title = "按钮";
    var textNode = document.createTextNode("text");
    button.appendChild(textNode);
    document.body.appendChild(button);
  }
</script>
<body>
  <div id="#id"></div>
  <div class="className"></div>
  <div name="name"></div>
  <button onclick="fun()">click</button>
</body>
```


## 事件
### 鼠标事件
- onclick	鼠标点击事件
- onmouseover	鼠标移入事件
- onmouseout	鼠标移出事件
- onmousedown	鼠标按下事件
- onmouseup	鼠标松开事件
- onmousemove	鼠标移动事件

```html
<script>
  window.onload = function () {
    var div = document.getElementById("item");
    div.onclick = function(){
        this.style.background = "red";
    }
    div.onmouseover = function(){
        this.style.background = "blue";
    }
    div.onmouseout = function(){
        this.style.background = "green";
    }
    div.onmousedown = function(){
        this.style.background = "yellow";
    }
    div.onmouseup = function(){
        this.style.background = "orange";
    }
    div.onmousemove = function(){
        this.style.background = "purple";
    }
  };
</script>
```

### 键盘事件
- onkeydown：键盘按下会触发的事件。
- onkeyup：键盘松开会触发的事件。
```html
<script>
  window.onload = function () {
    var val = document.getElementById("id");
    val.onkeydown = function () {
      this.style.color = "#00adb5";
    };
    val.onkeyup = function () {
      this.style.color = "red";
    };
  };
</script>
<body>
  <input type="text" id="id"/>
</body>
```

### 表单事件
- onfocus	表单元素聚焦时触发。
- onblur	表单元素失焦时触发。
```html
<script>
  window.onload = function () {
    var val = document.getElementById("id");
    val.onfocus = function () {
      this.style.color = "blue";
    };
    val.onblur = function () {
      this.style.color = "red";
    };
  };
</script>
<body>
  <input type="text" id="id"/>
</body>
```

### event事件对象
通过事件对象的属性，我们可以了解一个事件的详细情况
- type	查看事件类型
- shiftKey	是否按下 shift 键
- ctrlkey	是否按下 ctrl 键
- altkey	是否按下 alt 键
```html
<script>
  window.onload = function () {
    var btn = document.getElementById("btn");
    btn.onclick = function (e) {
      console.log("这是一个" + e.type + "事件"); // 控制台打印事件类型
    };
    var text = document.getElementById("item");
    var p = document.getElementById("item1");
    text.onkeydown = function (e) {
      // 判断键入的是否为 shift、alt、ctrl
      if (e.shiftKey || e.altKey || e.ctrlKey) {
        p.innerHTML = "不能键入 shift|alt|ctrl";
        p.style.color = "red";
        // 当键入的不为 shift、alt、ctrl 时，输出你的键入码
      } else {
        p.innerHTML = "你输入的键值码为：" + e.keyCode;
        p.style.color = "black";
      }
    };
  };
</script>
<body>
  <input type="button" value="点击" id="btn" />
  <input type="text" id="item" />
  <p id="item1"></p>
</body>
```

### DOM 0 级事件与 DOM 2 级事件
- DOM 0 级事件
  每个事件只能有一个响应方法
```html
<body>
  <input
    id="btn"
    type="button"
    value="点我"
    onclick="alert('第一个方法')"
  />
  <script>
    document.getElementById("btn").onclick = function () {
      alert("覆盖第一个方法");
    };
  </script>
</body>
```
- DOM 2 级事件
  每个事件可以有多个响应方法
  - 事件种类，响应函数，响应函数在事件之前还是之后运行
  - addEvenetListener(type,listener[,useCapture]); 添加事件
  - removeEventListener(type,listener[,useCapture]); 移出事件
```html
<body>
  <input id="btn" type="button" value="点我" />
  <script>
      var btn = document.getElementById("btn");
      btn.onclick = function () {
      alert("方法1");
      };
      btn.addEventListener("click", function () {
        alert("方法2");
      });
      btn.addEventListener("click", handler, false);
      function handler() {
        alert("方法3（只实现一次）");
        document
          .getElementById("btn")
          .removeEventListener("click", handler, false);
      }
  </script>
</body>
```

## AJAX
- 异步 JavaScript 和 XML，是一种创建交互式网页应用的网页开发，实现异步Http请求的技术。
```html
<script>
  window.onload = function () {
    if (window.XMLHttpRequest) {
      // Mozilla，Safari，IE7+ 等浏览器适用
      var httpRequest = new XMLHttpRequest();
    } else if (window.ActiveXObject) {
      // IE 6 或者更老的浏览器适用
      var httpRequest = new ActiveXObject("Microsoft.XMLHTTP");
    }
    // 规定发送请求的一些要求
    httpRequest.open(
      "GET",
      "https://jsonplaceholder.typicode.com/users",
      true
    );
    // 将请求发送到服务器
    httpRequest.send();
    httpRequest.onreadystatechange = function () {
      console.log("准备状态:" + httpRequest.readyState);
      console.log("状态码:" + httpRequest.status);
      if (httpRequest.readyState == 4 && httpRequest.status == 200) {
        // 请求成功执行的代码
        document.getElementById("item").innerHTML = "请求成功";
      } else {
        // 请求失败执行的代码
        document.getElementById("item").innerHTML = "请求失败";
      }
    };
  };
</script>
```

## 正则表达式
### 常用表达式
- `[a-z]`	查找任何从小写 a 到小写 z 的字符
- `[0-9]`	查找任何从 0 至 9 的数字
- `[abc]`	查找括号内的任意一个字符
- `[^abc]`	查找除了括号内的任意字符


### 常用元字符
- `\w`	匹配数字、字母、下划线（`\W`为相反条件）
- `\d`	匹配数字（`\D`为相反条件）
- `\s`	匹配空白字符（空格、换行）（`\S`为相反条件）
- `\n`	匹配换行符


### 常用限定符
- `*`	匹配前面的子表达式>=0次
- `+`	匹配前面的子表达式>=1次
- `?`	匹配前面的子表达式0次或1次
- `{n}` 匹配确定的 n 次
- `{n,}` 至少匹配 n 次
- `{n,m}` 最少匹配 n 次且最多匹配 m 次

### 常用修饰符
- `i`	执行对大小写不敏感的匹配。
- `g`	执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。
- `m`	执行多行匹配。

### 其他
- `^`	以...开始
- `$`	以...结束

```html
<script>
  window.onload = function () {
    var userForm = document.getElementById("userForm");
    var usernameText = document.getElementById("username");
    var msg = document.getElementById("msg");
    var btn1 = document.getElementById("btn1");
    btn1.onclick = function () {
      var regExp = /^[a-zA-Z]{6,10}$/;
      if (!regExp.test(username.value)) {
        msg.innerHTML = '<b style="color:red;">用户名格式不正确</b>';
      } else {
        // 提交表单
        userForm.submit();
      }
    };
  };
  function isEmail(email) {
    //验证规则：5-10个字符@1个或多个以上字符，以com、net、org结尾
    var regExp = /^\w{5,10}@\w+\.(com|net|org)$/;
    var flag = regExp.test(email);
    return flag;
  }
</script>
```

## 判断数据类型
- 基础数据类型
  - boolean
  - number
  - string
  - bigint
  - undefined
  - symbol
  - null（使用`target===null`判断）
    - null为全0，object前三位为0，被typeof错误识别
- 引用类型
  - object
  - function
  - regexp
  - date
  - error
  - array
  - map
  - set
  - weakmap
  - weakset
```js
function getType(target) {
  // 先进行 typeof 判断，如果是基础数据类型，直接返回。
  const type = typeof target;
  if (type !== "object") {
    return type;
  }
  // 如果是引用类型或者 null，再进行如下的判断，正则返回结果，注意最后返回的类型字符串要全小写。
  return Object.prototype.toString
    .call(target)
    .replace(/^\[object (\S+)\]$/, "$1")
    .toLocaleLowerCase();
}
```
- instanceOf
  - 用来判断prototype的类型
  - 只能判断引用类型

## Symbol
用来防止对象属性名冲突问题
```js
const obj = {
  name: "lin",
  age: 18,
};
const name = Symbol("name");

obj[name] = "xxx"; // 使用 Symbol，不会覆盖

console.log(obj); // { name: 'lin', age: 18, Symbol(name): 'xxx' }
console.log(obj.name); // 'lin'
console.log(obj[name]); // 'xxx'
```


## 判断对象是否为空
- for
  - 如果能被遍历，说明这个对象有属性，返回 false
```js
function isEmptyObject(obj) {
  for (let o in obj) {
    return false;
  }
  return true;
}
```

- Object.keys()
  - 把对象转化为数组，然后再根据数组的长度是否为零来判断对象是否为空。
```js
function isEmptyObject(obj) {
  return Object.keys(obj).length === 0;
}
```
但是不能解决null 或 undefined
所以修改为
```js
function isEmptyObject(obj) {
  return Object.keys(obj || []).length === 0;
}
```

## 防抖函数
使用该函数包装fn函数，当fn被多次调用后，只会在最后一次调用后的delay秒后运行
```js
function debounce(fn, delay = 0) {
  // 返回一个新的防抖函数
  // 即使函数在 delay 时间段内多次被调用，也只会在最后一次函数被调用的 delay 时间结束后执行
  let time;
  return function(args){
    clearTimeout(time);
    time = setTimeout(() => {
      fn.call(this, args);//此处this没有具体指向，可能是指向调用fn的对象，也可能是使用call指定该函数的对象
    }, delay);
  }
}
```

## this
### 全局中的函数
全局直接调用的函数或语句的 this 指向 window
- 在严格模式下函数指向的 this为 undefined

### 对象中的函数
#### 调用对象中的函数中使用 this，指向对象本身
```js
const obj = {
  a: 1,
  fn() {
    console.log("this :>> ", this); // 输出 obj
    console.log("this.a :>> ", this.a); // 输出 1
  },
};
obj.fn();
```
#### 返回值为函数，则 this 指向调用函数的主体
```js
const obj = {
  a: 1,
  fn() {
    return function () {
      console.log("this :>> ", this); // 输出 window
      console.log("this.a :>> ", this.a); // 输出 100
    };
  },
};
var a = 100;
obj.fn()();//指向window
```
```js
const o1 = {
  text: "o1",
  fn() {
    return this.text;
  },
};

const o2 = {
  text: "o2",
  fn() {
    return o1.fn();
  },
};

const o3 = {
  text: "o3",
  fn() {
    var fn = o1.fn;
    return fn();
  },
};

console.log(o1.fn()); // o1
console.log(o2.fn()); // o1
// 等同于执行o1.fn()
console.log(o3.fn()); // undefined
// 等同于复制o1函数执行过程并返回，也就是由window来执行该函数 
```
```js
function foo() {
  return () => {
    console.log(this.a);
  };
}

const obj1 = {
  a: 2,
};

const obj2 = {
  a: 3,
};

const bar = foo.call(obj1);
// 正常调用call函数，绑定obj1的值，返回一个绑定后的箭头函数
bar.call(obj2); // 输出2
// bar中存在已经绑定过的箭头函数，箭头函数不能修改绑定，所以输出obj1的值
```


##### 解决方法
- ES6 之前使用新变量存储当前 this，不调用函数中 this
```js
const obj = {
  a: 1,
  fn() {
    const _this = this;
    return function () {
      console.log("this :>> ", _this); // 输出 obj
      console.log("this.a :>> ", _this.a); // 输出 1
    };
  },
};
obj.fn()();
```
- ES6之后使用匿名函数解决，匿名函数只会从自己的作用域链的上一层继承 this
```js
const obj = {
  a: 1,
  fn() {
    return () => {
      console.log("this :>> ", this); // 输出 obj
      console.log("this.a :>> ", this.a); // 输出 1
    };
  },
};
obj.fn()();
```
### 构造函数中的 this
#### 如果返回值是一个对象，this 指向返回值的对象，否则 this 指向函数新建的实例
```js
function Person(name) {
  this.name = name;
}
const p = new Person("zhangsan");
console.log(p.name); // 'zhangsan'
```
```js
function Person(name) {
  this.name = name;
  return {
    name: "xxx",
  };
}
const p = new Person("zhangsan");
console.log(p.name); // 'xxx'
```
```js
function Person(name) {
  this.name = name;
  return {};
}
const p = new Person("zhangsan");
console.log(p.name); // 'undefined'
```

#### 如果返回值不是一个对象，this 还是指向实例本身
```js
function Person(name) {
  this.name = name;
  return 123;
}
const p = new Person("zhangsan");
console.log(p.name); // 'zhangsan'
```

### 修改函数上下文的 this
#### call 方法
使用方法`fun.call(对象名，参数...)`，将`fun函数`在`该对象`上调用
```js
function fn() {
  console.log(this.name);
}

const obj = {
  name: "zhangsan",
};
fn.call(obj); // 指定 this 为 obj，输出 'zhangsan'
```

#### apply 方法
和 call 方法功能一样，参数不同，call 接受多个参数，apply 接受参数数组
```js
function add(x, y, z) {
  return this.x + this.y + this.z;
}

const obj = {
  x: 1,
  y: 2,
  z: 3,
};

console.log(add.call(obj, 1, 2, 3)); // 输出 6
console.log(add.apply(obj, [1, 2, 3])); // 输出 6，只是传参形式不同而已
```

#### bind 方法
和 call 区别为 bind 方法返回一个参数和this构造好的函数，但不会执行，需要手动执行
```js
function add(x, y, z) {
  return this.x + this.y + this.z;
}

const obj = {
  x: 1,
  y: 2,
  z: 3,
};

const add1 = add.bind(obj, 1, 2, 3); // bind 会返回一个新的函数
console.log(add1()); // 执行新的函数，输出 6
```

# Vue

## 创建实例
- 在 `head` 区域引入本地 `Vue.js` 或使用 `CDN` 引入 `Vue.js`
```js
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.10/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.10"></script>
```

- 在 `script` 中使用以下语句创建 `Vue` 实例
```js
var app = new Vue({
  // 选项
  el: "#app", //绑定的 id 名
  data: { //数据
    class-to-add: "1111",
    url: "https://www.lanqiao.cn",
    isChecked: true
  },
});
```

## 插入文本

- 使用双大括号进行插入数据
```html
<div id="app">msg：{{msg}}</div>
```

- 加入 `v-once` 指令可使得插入数据为一次性不可更改
```html
<p v-once>msg：{{msg}}</p>
```

- 提供了完全的 `JavaScript` 表达式支持
```html
<p>num + 24 = {{num + 24}}</p>
<!-- 三元表达式 -->
<p>Are you ok? {{ok ? 'I am ok !':'no'}}</p>
<!-- 对象方法直接调用 -->
<p>名字倒过来写：{{name.split('').reverse().join('')}}</p>
<!-- 属性值运算操作 -->
<p v-bind:class="'col'+colNum">syl</p>
```

## 指令 Directives

### 简单指令
- 加入 `v-html` 指令可使得插入数据按照 `html` 格式显示
```html
<div id="app" v-html="msg"></div>
```

- 加入 `v-bind` 指令可以在标签上插入数据
  - 缩写为 `:`
  - 如果 `isChecked` 的值是 `null`、`undefined` 或 `false`，则 `checked` 特性甚至不会被包含在渲染出来的`<input>`元素中
```html
<div id="app">
  <div v-bind:class="class-to-add"></div>
  <div :class="class-to-add"></div>
  <a v-bind:href="url">实验楼</a>
  <input type="checkbox" v-bind:checked="isChecked"/>
</div>
```
```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      class-to-add: "1111",
      url: "https://www.lanqiao.cn",
      isChecked: true
    },
  });
</script>
```

- 使用 `v-on` 指令，用于监听 `DOM` 事件
  - 缩写为 `@`
  - 指令中的属性可以为动态确定的
```html
<div id="app">
  <p>我叫：{{name}}</p>
  <!-- handleClick 使我们在实例 methods 中写的方法 -->
  <button v-on:click="handleClick">点我</button>
  <button @click="handleClick">点我</button>
  <button v-on:[event]="handleClick">点我</button>
</div>
```
```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      name: "实验楼",
      event: "click",
    },
    methods: {
      // 实例方法对象
      handleClick: function () {
        this.name = this.name.split("").reverse().join("");
      },
    },
  });
</script>
```

### 修饰符
修饰符是以点开头的特殊后缀，表明指令需要以一些特殊的方式被绑定
- `.prevent` 修饰符会告知 `v-on` 指令对触发的事件调用 `event.preventDefault()`
```html
<div id="app">
  <form action="/" v-on:submit.prevent="submit">
    <button type="submit">提交</button>
  </form>
</div>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {},
    methods: {
      submit: function () {
        console.log("成功提交！");
      },
    },
  });
</script>
```