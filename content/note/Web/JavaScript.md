---
title: JavaScript笔记
tags:
  - Note
  - Web
  - JavaScript
date: 2023-12-23
description: 关于JavaScript的语法
slug: javascript-note
---
# 属性

- classList: 用于获取或修改元素的类列表。
  - 使用 add, remove 添加删除类名，使用 contains 检查是否包含某个类名，使用 toggle 切换类名。
- id: 元素的唯一标识符。
- style: 元素的内联样式属性。
  - `visibility` 控制元素的可见性
    - `hidden`
    - `visible`
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

# 本地存储

- `localStorage` 永久存储
- `sessionStorage` 仅在当前会话下有效
  - `setItem(key,value)` 保存数据到本地存储
  - `getItem(key)` 从本地存储获取数据
  - `removeItem(key)` 根据指定 key 从本地存储中移除数据
  - `clear()` 清除所有保存数据
- `localstorage`与`cookie`的区别：
  -localStorage 解决了早期使用 cookie 存储遇到的存储空间不足的问题( 每条 cookie 的存储空间为 4k)；
  -localStorage 一般浏览器支持的是 5M 大小，具体存储大小根据浏览器的不同会有所不同
  - 并且相较于 cookie 而言，localStorage 中的信息不会被传输到服务器
- 那么`localStorage`和`sessionStorage`区别
  - `localStorage` 的生命周期是永久的，除非用户清除 localStorage 信息，否则这些信息将永远存在
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

# 运算符

- `===`左右两边的操作数相等且类型相同时，返回 true
- `!==`左右两边的操作数不相等或者类型不相同时，返回 true

# 循环

- `for`遍历
  - `for(i in arr){}`等效于`for(var i = 0; i < arr.length; i++){}`

# 函数

```js
function 函数名(参数){
  ...
  return 返回值;
}
```

## 链式调用

如果返回值为一个函数，则可以继续通过括号当作函数传参调用

```js
function f(...args){
  return (...arg1) => arg1.length ? f(args, arg1) : `参数：${args.join(',')}`;
}

f(param1)(param2)(param3)();
```

# 数组

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

# 容器

## Map

## Set

### 可接受参数

- 数组：将数组中的每个元素作为 Set 对象的一个唯一值。
- 字符串：将字符串中的每个字符作为 Set 对象的一个唯一值。
- Set 对象：将另一个 Set 对象中的所有唯一值复制到新的 Set 对象中。
- 其他可迭代对象：可以是实现了迭代器接口的对象，如 Map、TypedArray 等，将其迭代的每个元素作为 Set 对象的一个唯一值。

# 字符串 String

- `str.length`获取长度
- `str.toLowerCase()`大写转小写
- `str.toUpperCase()`小写转大写
- `str.charAt(index);`获取指定下标的字符
- `str.substring(start,end);`获取指定下标区间内的字符
- `str.replace(oldstr,newstr);`替换部分字符串
  - `oldstr`部分可使用正则表达
  - `str.replace(regex, (match, offset) => {return newstr});`获取偏移量和自定义替换结果
- `str.split("分隔符");`分割字符串成数组
- `str.indexOf(str);`查找 str 首次出现的下标

# `String` 和 `数字` 转换

## String 转数字

- parseFloat(str)
- parseFloat(str.match(/\d+\.\d+/)[0]);

# 定时器

- setInterval 设置每多长时间重复一次

```js
setInterval(function() {
  console.log("Hello, world!");
}, 1000);
```

- clearInterval 清除计时器

```js
// 定义一个周期性执行的函数
function sayHello() {
  console.log("Hello, world!");
}

// 每隔一秒执行一次 sayHello 函数
var intervalID = setInterval(sayHello, 1000);

// 5 秒后停止执行 sayHello 函数
setTimeout(function() {
  clearInterval(intervalID); // 停止周期性执行
}, 5000);
```

- setTimeout 设置多长时间后执行一次

```js
setTimeout(function() {
  console.log("Hello, world!");
}, 3000);
```

# 库

## Math

- `Math.E` 自然对数的底数
- `Math.LN2` 2 的自然对数
- `Math.PI` 圆周率
- `Math.SQRT2` 2 的平方根
- `Math.abs(x)` 返回一个数的绝对值
- `Math.pow(x,y)` 返回一个数的 y 次幂
- `Math.random()` 返回一个 0 到 1 之间的伪随机数
- `Math.sqrt(x)` 返回一个数的平方根
- `Math.round()` 返回四舍五入后的整数
- `Math.exp(x)` 返回欧拉常数的参数次方

## Date

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

# BOM(Browser Object Model)

是浏览器对象模型，通过操作对象的属性和方法来实现与浏览器的交互

- BOM 组成
  - document 是 DOM 对象。
  - location 是用于获取或设置窗体。
  - navigation 包含浏览器配置相关的信息。
  - history 浏览器的历史记录。
  - screen 用于显示设备信息。
- 方法
  - `alert()` 显示一个警告框。
  - `prompt()` 显示可提示用户输入的对话框。
  - `confirm()` 显示一个有确认和取消按钮的对话框。
  - `open()` 打开一个新的浏览器页面。
  - `close()` 关闭浏览器页面。
  - `print()` 打印当前窗口内容。

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

# DOM(Document Object Model)

它是浏览器为每个窗口内的 HTML 页面创建的一个 document 对象，用来对页面的元素进行操作

- `document.title` 获取文档的 title 元素
- `document.body` 获取文档的 body 元素
- `document.URL` 获取文档的 URL
- `document.forms` 获取文档的 form 元素
- `document.images` 获取文档的 img 元素
- `document.links` 获取文档的 a 元素
- `document.cookie` 获取文档的 cookie
- `document.referrer` 返回来用户当前浏览页面的 URL
- `document.getElementById()` 通过 id 获取元素
- `document.getElementsByClassName()` 通过 class 获取元素
- `document.getElementsByName()` 通过 name 获取元素
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

# 事件

## 鼠标事件

- onclick 鼠标点击事件
- onmouseover 鼠标移入事件
- onmouseout 鼠标移出事件
- onmousedown 鼠标按下事件
- onmouseup 鼠标松开事件
- onmousemove 鼠标移动事件

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

## 键盘事件

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

## 表单事件

- onfocus 表单元素聚焦时触发。
- onblur 表单元素失焦时触发。

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

## event 事件对象

通过事件对象的属性，我们可以了解一个事件的详细情况

- type 查看事件类型
- shiftKey 是否按下 shift 键
- ctrlkey 是否按下 ctrl 键
- altkey 是否按下 alt 键

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

## DOM 0 级事件与 DOM 2 级事件

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

# AJAX

- 异步 JavaScript 和 XML，是一种创建交互式网页应用的网页开发，实现异步 Http 请求的技术。

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

# 正则表达式

## 常用表达式

- `[a-z]` 查找任何从小写 a 到小写 z 的字符
- `[0-9]` 查找任何从 0 至 9 的数字
- `[abc]` 查找括号内的任意一个字符
- `[^abc]` 查找除了括号内的任意字符

## 常用元字符

- `\w` 匹配数字、字母、下划线（`\W`为相反条件）
- `\d` 匹配数字（`\D`为相反条件）
- `\s` 匹配空白字符（空格、换行）（`\S`为相反条件）
- `\n` 匹配换行符

## 常用限定符

- `*` 匹配前面的子表达式>=0 次
- `+` 匹配前面的子表达式>=1 次
- `?` 匹配前面的子表达式 0 次或 1 次
- `{n}` 匹配确定的 n 次
- `{n,}` 至少匹配 n 次
- `{n,m}` 最少匹配 n 次且最多匹配 m 次
- `(...)` 捕获组
- `(?:...)` 非捕获组，用于将内容打包成一组执行其它匹配操作

## 常用修饰符

- `i` 执行对大小写不敏感的匹配。
- `g` 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。
- `m` 执行多行匹配。

## 其他

- `^` 以...开始
- `$` 以...结束

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
    var match = regExp.exec(email);
    console.log(match[0]);//输出匹配到的字符
    return flag;
  }
</script>
```

# 判断数据类型

- 基础数据类型
  - boolean
  - number
  - string
  - bigint
  - undefined
  - symbol
  - null（使用`target===null`判断）
    - null 为全 0，object 前三位为 0，被 typeof 错误识别
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
  - 用来判断 prototype 的类型
  - 只能判断引用类型

# Symbol

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

# Proxy

用于创建一个对象的代理，从而实现基本操作的拦截和自定义（如属性查找、赋值、枚举、函数调用等）

```js
var proxy = new Proxy(target, {
  get(obj, key) { //当获取 target 内属性时会运行该函数
    return obj[key];
  },
  set(obj, key, value) { //当设置 target 内属性时会运行该函数
    obj[key] = value;
    if (key === "age") {
      if (value > 150) {
        obj[key] = 150;
      } else if (value < 0) {
        obj[key] = 0;
      }
    }
  }
})
```

# filter

创建给定数组一部分的浅拷贝，返回满足给定函数的所有元素

- `arr.filter(callbackFn)`
  - `callbackFn` 用于测试的函数

```js
const newArr = arr.filter(item => item > 0);
```

# map(Array 内置函数)

创建一个新数组，这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成。

- `map(callbackFn)`
  - `callbackFn` 用于测试的函数

```js
const newArr = arr.map(item => {
    // item 处理
    return item;
  });
```

## `map`和 `filter` 区别

- `map` 返回的数组每个元素由 `return` 的值组成
- `filter` 返回的数组每个元素为原来的元素，是否存到新数组中由 `return`的布尔值确定

# 判断对象是否为空

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

但是不能解决 null 或 undefined
所以修改为

```js
function isEmptyObject(obj) {
  return Object.keys(obj || []).length === 0;
}
```

# 防抖函数

使用该函数包装 fn 函数，当 fn 被多次调用后，只会在最后一次调用后的 delay 秒后运行

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

# this

## 全局中的函数

全局直接调用的函数或语句的 this 指向 window

- 在严格模式下函数指向的 this 为 undefined

## 对象中的函数

### 调用对象中的函数中使用 this，指向对象本身

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

### 返回值为函数，则 this 指向调用函数的主体

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

#### 解决方法

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

- ES6 之后使用匿名函数解决，匿名函数只会从自己的作用域链的上一层继承 this

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

## 构造函数中的 this

### 如果返回值是一个对象，this 指向返回值的对象，否则 this 指向函数新建的实例

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

### 如果返回值不是一个对象，this 还是指向实例本身

```js
function Person(name) {
  this.name = name;
  return 123;
}
const p = new Person("zhangsan");
console.log(p.name); // 'zhangsan'
```

## 修改函数上下文的 this

### call 方法

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

### apply 方法

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

### bind 方法

和 call 区别为 bind 方法返回一个参数和 this 构造好的函数，但不会执行，需要手动执行

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
