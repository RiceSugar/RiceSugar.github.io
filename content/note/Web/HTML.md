---
title: HTML笔记
tags:
  - Note
  - Web
  - HTML5
date: 2023-12-23
description: 关于HTML5的语法
slug: html-note
---
# 信息文件 head

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

# 内容主体 body

# 元素类型

## 行级元素

行级元素不会独占一行，只占据它对应标签的边框所包含的空间

- `<span>`: 用于对文本进行分组，是最通用的行内元素。
- `<a>`: 表示超链接。
- `<strong>`, `<em>`: 分别表示强调文本的重要性和斜体文本。
- `<img>`: 表示图像。
- `<br>`: 表示换行。
- `<input>`: 表示输入框。
- `<button>`: 表示按钮。
- `<label>`: 用于标记表单元素。

## 块级元素

块级元素会独占一行，会完全占满父元素的内容区域

- `<div>`: 用于定义文档中的分区或节，是最通用的块级元素。
- `<p>`: 表示段落。
- `<h1>, <h2>, ..., <h6>`: 表示标题，依次为从大到小的标题。
- `<ul>, <ol>, <li>:` 表示无序列表和有序列表。
- `<table>`: 表示表格。
- `<form>`: 表示表单。
- `<header>`, `<footer>`, `<nav>`, `<article>`: HTML5 中的语义块级元素，用于定义页面结构。
- `<section>`, `<aside>`, `<main>`: HTML5 中的语义块级元素，用于更具体的页面结构。

# 标题

```html
<h1>This is a heading</h1>
<h2>This is a heading</h2>
```

# 段落

```html
<p>This is a paragraph.</p>
```

# 链接

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

# span 盒子

在同一行里放多个 span 盒子

```html
<span style="color: chocolate; background-color: bisque;">This is a span</span>
```

# 强调

```html
<strong>加粗强调</strong>
```

# 图像

```html
<img src="image.jpg" alt="图像描述" width="12" height="10"/>
```

# div 盒子

每个盒子独占一行

```html
<div style="color: chocolate; background-color: bisque;">This is a div</div>
```

# 列表

- type 属性修改列表的样式
  - 1 数字
  - a 小写字母
  - A 大写字母
  - i 小写罗马数字
  - I 大写罗马数字
- start 属性修改起始号

```html
<ol>
    <li>有序列表</li>
    <li>有序列表</li>
    <li>有序列表</li>
</ol>
```

- type 属性修改列表的样式
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

# 表格

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

# 表单

- 表单用于向服务器传输数据
  - action 提交地址
  - method 提交方式
  - autocomplete 自动填充

```html
<form action="http://www.biadu.com" method="get" autocomplete="on">

</form>
```

## 表单项

### input 标签

#### type 属性

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

#### 其他属性

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

### select 下拉列表

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

### textarea 文本域

- cols 列数
- rows 行数

```html
<form>
  文本域：
  <textarea name="area1" cols="30" rows="10">hello，world</textarea>
</form>
```

# 语义化标签

- header 标签是头部区域
- nav 标签是导航区域
- article 标签是内容区域
- section 标签是文档中部分内容区域
- aside 标签是侧边内容栏区域
- footer 标签是底部信息区域

# audio 音频标签

- controls 用于提供播放、暂停和音量控件
- autoplay 自动播放
- loop 循环播放

```html
<audio src="./music.mp3" controls="controls" autoplay="autoplay" loop="loop"></audio>
```

- source 标签
  可设置多个数据源

```html
<audio>
  <source src="./music.mp3" type="audio/mp3">
  <source src="./music.ogg" type="audio/ogg">
</audio>
```

# video 视频标签

- muted 静音
- poster 封面

```html
<video controls muted poster="./poster.jpg">
  <source src="./video.mp4" />
</video>
```
