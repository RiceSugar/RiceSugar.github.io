---
title: Vue笔记
tags:
  - Note
  - Web
  - Vue
date: 2023-12-23
description: 含有Vue的语法
slug: vue-note
---

# 创建实例

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

# 插入数据

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

# 指令 Directives

## 简单指令

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

## 修饰符

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

# 计算属性 computed

当 `value` 改变时触发 `function`，是 **惰性** 的，当依赖数据发生改变时，才会触发计算，否则，它的值是上一次触发计算的缓存值

> computed: {
> value: function(){};
> }

```html
<body>
  <div id="app">{{now}}</div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {},
      computed: {
        now: function () {
          return Date.now();
        },
      },
    });
  </script>
</body>
```

## getter 和 setter

> computed: {
> value: {
> get: function () {},
> set: function (newName) {},
> },
> }

```html
<body>
  <div id="app">
    <p>firstName:{{firstName}}</p>
    <p>lastName:{{lastName}}</p>
    <p>全名是:{{fullName}}</p>
    <button v-on:click="changeName">改姓</button>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        firstName: "王",
        lastName: "花花",
      },
      methods: {
        // changeName 定义一个方法改变 计算属性 fullName 的值
        changeName: function () {
          // 修改计算属性 fullName 等于李花花
          this.fullName = "李花花";
          // 上面一句等于触发了 fullName 属性的 setter
        },
      },
      computed: {
        fullName: {
          // getter
          get: function () {
            return this.firstName + this.lastName;
          },
          // setter  直接改变计算属性 fullName 的值就可以触发 setter this.fullName='XX'
          set: function (newName) {
            var name = newName;
            this.firstName = name.slice(0, 1); // 取新值的第一个字符
            this.lastName = name.slice(1); // 从新值的第二个字符开始取值
          },
        },
      },
    });
  </script>
</body>
```

# 侦听属性 watch

当 `value` 改变时触发 `function`，参数提供改变后的新值和改变前的旧值

> watch: {
> value: function (newVal, oldVal) {}
> }

```html
<body>
  <div id="app">
    <p>{{msg}}</p>
    <!-- v-on:click 简写为 @click -->
    <button @click="handleClick('hello syl')">改变msg</button>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        msg: "hello",
      },
      methods: {
        // 改变 msg 的值
        handleClick: function (val) {
          this.msg = val;
        },
      },
      // watch 监听属性
      watch: {
        // 监听新旧值  监听属性有两个参数，第一个新值，第二个旧值
        msg: function (newVal, oldVal) {
          alert("新值" + newVal + "----" + "旧值" + oldVal);
        },
      },
    });
  </script>
</body>
```

- 通常来说能用计算属性代替就用计算属性代替，多大情况计算属性代码更精简，可读性更高

# 过滤器 filters

放在 **双花括号** 和 **v-bind 表达式** 中

```html
<body>
  <div id="app">
    <!-- toUpperCase   getString  为自定义的过滤器-->
    <p>小写转换大写：过滤前：{{msg}} 过滤后： {{msg|toUpperCase}}</p>
    <p>去除数字：过滤前：{{msg2}} 过滤后： {{msg2|getString}}</p>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        msg: "hello",
        msg2: "1s2y3l",
      },
      filters: {
        // toUpperCase 定义一个字符串转大写的过滤器
        toUpperCase: function (val) {
          return val.toUpperCase();
        },
        // getString 定义一个获取去除数字的过滤器
        getString: function (val) {
          let newVal = "";
          val.split("").map(function (item) {
	        // item 隐式转换为整数类型
            if (9 >= item && item >= 0) {
              return;
            } else {
              return (newVal += item);
            }
          });
          return newVal;
        },
      },
    });
  </script>
</body>
```

# 响应式

```js
let {value} = {...data}
// 单纯{...data} 没有响应式布局 ref的才可以直接value
let {value} = {...toRefs(data)}
// 所以通过torefs(data)转为ref响应式布局
console.log({...toRefs(data)})
console.log(data)
```

# v-bind

## 绑定 class

- 给  `v-bind:class`  一个对象，以动态地切换 `class`，`class` 存在与否将取决于数据属性  `isActive`  的 Boolean 值，语法为  `{className:Boolean}`，`v-bind:class` 可兼容普通 `class`

```html
<style>
  .active {
    color: pink;
    font-size: 22px;
  }
  .red-bg {
    background: red;
  }
</style>
```

```html
<div id="app">
  <!-- 数组语法绑定 class 当 isActive 为 true 时，active 就成 span 标签的 class -->
  <span class="static" :class="{'active':isActive,'red-bg':isRed}"
    >syl</span>
  <!-- isActive 为 true 渲染后 <span class="static active red-bg">syl</span> -->
</div>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      isActive: true,
      isRed: true,
    },
  });
</script>
```

- 可以把一个数组传给  `v-bind:class`，以应用一个 class 列表

```html
<style>
  .active {
    color: pink;
    font-size: 22px;
  }
  .red-bg {
    background: red;
  }
</style>
```

```html
<div id="app">
  <!-- 数组语法绑定 class -->
  <span v-bind:class="[activeClass,bgColorClass]">syl</span>
  <!-- 渲染后 <span class="active red-bg">syl</span> -->
</div>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      activeClass: "active",
      bgColorClass: "red-bg",
    },
  });
</script>
```

## 绑定 style

- 使用 `v-bind:style` 绑定样式

```html
<div id="app">
  <p v-bind:style="{fontSize:size,backgroundColor:bgColor}">你好，实验楼</p>
</div>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      size: "26px",
      bgColor: "pink",
    },
  });
</script>
```

- 可以绑定到样式对象

```html
<div id="app">
  <p v-bind:style="styleObject">你好，实验楼</p>
</div>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      styleObject: {
        fontSize: "26px",
        backgroundColor: "pink",
      },
    },
  });
</script>
```

- 可以用数组将多个样式对象应用到同一个元素上

```html
<div id="app">
  <p v-bind:style="[styleObject1,styleObject2]">你好，实验楼</p>
</div>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      //样式一
      styleObject1: {
        fontSize: "26px",
        backgroundColor: "pink",
      },
      //样式二
      styleObject2: {
        marginTop: "200px",
        textAlign: "center",
      },
    },
  });
</script>
```

## 属性自动绑定

由于浏览器内核不同，使用某些 CSS 属性需要带各浏览器的前缀，然而`v-bind:style`  会自动给需要前缀的属性加前缀

## 动态切换

```html
<style>
  .active {
    color: red;
  }
</style>
<div id="app">
  <p
    v-bind:style="{fontSize:fontSize+'px'}"
    v-bind:class="{active:isActive}"
  >
    你好，实验楼
  </p>
  <button @click="handleClick">变大变色</button>
</div>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
      fontSize: 20,
      isActive: true,
    },
    methods: {
      handleClick: function () {
        this.fontSize += 2;
        this.isActive = !this.isActive; // 取反
      },
    },
  });
</script>
```

# v-if

`v-if`  指令用于条件性地渲染一块内容

```html
<p v-if="display">你好，实验楼</p>
```

```html
<script>
  var app = new Vue({
    el: "#app",
    data: {
		display: true,
    },
  });
</script>
```

## v-else

- `v-else`  元素必须紧跟在带  `v-if`  或者  `v-else-if`  的元素的后面，否则它将不会被识别

```html
<div id="app">
  <p v-if="display">你好，实验楼</p>
  <p v-else>SYL</p>
</div>
```

# v-show

- `v-show`  的元素始终会被渲染并保留在 DOM 中。`v-show`  只是简单地切换元素的 CSS 属性  `display`。而  `v-if`  是从虚拟 DOM 的层面操作
- `v-if`  会牵涉到虚拟 DOM diff 算法，有更高的切换开销，而  `v-show`  有更高的初始渲染开销

```html
<body>
	<div id="app">
	  <p v-show="show">你好，实验楼</p>
	  <button @click="click">ok</button>
	</div>
	<script>
	  var app = new Vue({
	    el: "#app",
	    data: {
	      show: true,
	    },
	    methods: {
	        click(){
	            this.show = false;
	        }
	    }
	  });
	</script>
</body>
```

# v-for

## 渲染数组

此处 index 获取数组每项的下标

```html
<body>
	<div id="app">
	  <ul class="nav">
	    <li v-for="(navItem, index) in nav">{{navItem}}</li>
	  </ul>
	</div>
	<script>
	  var app = new Vue({
	    el: "#app",
	    data: {
	      nav: ["home", "shop", "contact", "about", "name", "mroe", "histroy"],
	    },
	  });
	</script>
</body>
```

- 数组可以为计算属性或方法的结果

```html
<body>
  <div id="app">
    <span v-for="number in oddNumber">{{number}}</span>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        numberArray: [1, 2, 3, 4, 5, 6, 7, 8],
      },
      computed: {
        // 计算 numberArray 中为奇数的 oddNumber 奇数数组
        oddNumber: function () {
          return this.numberArray.filter(function (number) {
            return number % 2 === 1;
          });
        },
      },
    });
  </script>
</body>
```

```html
<body>
  <div id="app">
    <!-- v-for 内直接调用方法 -->
    <span v-for="number in getOddNumber()">{{number}}</span>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        numberArray: [1, 2, 3, 4, 5, 6, 7, 8],
      },
      methods: {
        // 定一个一个获取数组内奇数的方法 filter 数组对象的过滤方法
        getOddNumber: function () {
          return this.numberArray.filter(function (number) {
            return number % 2 === 1;
          });
        },
      },
    });
  </script>
</body>
```

- 遍历的对象可以是数字

```html
<div id="app">
  <!-- :style 绑定样式 -->
  <span v-for="number in 10">{{number}} </span>
</div>
```

- 将对象数据渲染为元素，只能读出其中的`value`

```html
<body>
  <div id="app">
    <div v-for="val in userInfo">
      <p>{{val}}</p>
    </div>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        userInfo: {
          name: "whh",
          age: 1,
          sex: "woman",
        },
      },
    });
  </script>
</body>
```

## 使用 v-if 嵌套

```html
<body>
  <div id="app">
    <div v-if="numbers.length">
      <div v-for="item in numbers">{{item}}</div>
    </div>
    <div style="color:red" v-else>请添加数组元素</div>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
	        numbers: [1, 2, 3, 4],
      },
    });
  </script>
</body>
```

## 触发视图更新

- `Vue` 不能读取对象内部属性的改变，如果需要对象内部属性改变，同时触发视图更新，则需要使用`set(object, key, value)`方法赋值
- 用  `Vue.set(object, key, value)`  方法向嵌套对象添加响应式属性

```html
<body>
	<div id="app">
        <div v-for="val in userInfo">
          <p>{{val}}</p>
        </div>
        <button @click="click">ok</button>
    </div>
	<script>
	  var app = new Vue({
	    el: "#app",
	    data: {
          userInfo: {
            name: "whh",
          },
        },
        methods:{
            click(){
                Vue.set(this.userInfo,"name","naaaame");
            }
        }
	  });
	</script>
</body>
```

## 提供 key 属性

- 为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一  `key`  属性。理想的  `key`  值是每项都有的唯一 id

```html
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

- `key`  并不与  `v-for`  特别关联，建议尽可能在使用  `v-for`  时提供  `key`，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。

## 变异方法

- 这些数组操作方法，会直接改变原始数组，会促使视图自动更新。
  - `push()`
  - `pop()`
  - `shift()`
  - `unshift()`
  - `splice()`
  - `sort()`
  - `reverse()`
- 有些数组方法是不直接改变原数组的，称它们为非变异方法
  - 将非变异方法返回的新数组直接赋值给的旧数组以促使视图更新

```js
this.nav = this.nav.slice(1, 4);
```

- Vue 不能检测以下变动的数组
  - 当利用索引直接设置一个项时，例如：`vm.items[indexOfItem] = newValue`
  - 当修改数组的长度时，例如：`vm.items.length = newLength`
  - 可以用以下两种方法代替修改数组

```js
// Vue.set
Vue.set(app.items, indexOfItem, newValue);
// Array.prototype.splice
app.items.splice(indexOfItem, 1, newValue);
```

# v-on

> 给元素绑定事件监听器

Vue 中是虚拟 DOM，不太提倡直接进行原生 DOM 操作，会降低性能。在 Vue 中可以使用  `v-on`  指令来操作 DOM 事件

- 缩写：`@`

```html
<body>
  <div id="app">
    <!-- 绑定点击监听 -->
    <button v-on:click="say">点击</button>
    <button v-on:click="counter+=1">点击</button>
    <html>count:{{counter}}</html>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        counter: 0,
      },
      methods: {
        // 声明事件点击监听 say 方法
        say: function (event) {
          // 监听事件回调处理 event.type 触发事件类型 说明：`${}` 为 es6 模板字符串，拼接字符串的
          alert(`小楼提醒：你触发了${event.type}事件`);
        },
      },
    });
  </script>
</body>
```

## 事件修饰符

- `.stop`：阻止单击事件继续传播。
- `.prevent`：阻止事件默认行为。
- `.capture`：添加事件监听器时使用事件捕获模式。
- `.self`：只当在 event.target 是当前元素自身时触发处理函数。
- `.once`：点击事件将只会触发一次。
- `.passive`：滚动事件的默认行为 (即滚动行为) 将会立即触发。

```html
<body>
  <div id="app">
    <div class="super" v-on:click.stop="handleClick('super')">
      父
      <div class="child" v-on:click.stop="handleClick('child')">子</div>
    </div>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {},
      methods: {
        // 声明事件点击监听 handleClick
        handleClick: function (name) {
          alert(`我是${name}`);
        },
      },
    });
  </script>
</body>
```

### `keyup`相关

在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：

- .enter
- .tab
- .delete (捕获“删除”和“退格”键)
- .esc
- .space
- .up
- .down
- .left
- .right

```html
<body>
  <div id="app">
    <input type="text"
      v-on:keyup.enter="alert('你按了enter,确定输入完毕？')"/>
    <!-- 支持键码 -->
    <input type="text"
	  v-on:keyup.13="alert('你按了enter,确定输入完毕？')" />
  </div>
  <script>
    var app = new Vue({
      el: "#app",
    });
  </script>
</body>
```

### `click` 相关

可以用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。

- .ctrl
- .alt
- .shift
- .meta（windows 键）

```html
<body>
  <div id="app">
    <!-- 同时鼠标左击和按 ctrl 弹出提示 -->
    <div @click.ctrl="alert('你同时按了鼠标点击和ctrl')">Do something</div>
  </div>
</body>
```

- `.exact`  精确按键修饰符，严格限定按下的按键

```html
<div id="app">
  <!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
  <button @click.ctrl="alert('你不单单只按了鼠标左键和 Ctrl键，同时按其他键我也可以触发')">A</button>
  <!-- 有且只有 ctrl 键 + 鼠标左键 被按下的时候才触发 -->
  <button @click.ctrl.exact="alert('你只按ctrl键+鼠标左键，才能触发我')">A</button>
  <!-- 没有任何系统修饰符被按下的时候才触发 -->
  <button @click.exact="alert('没有按任何系统修饰符')">A</button>
</div>
```

限制处理函数仅响应特定的鼠标按钮

- `.left`
- `.right`
- `.middle`

```html
<div id="app">
  <button @click.left="alert('你按了鼠标左击键')">按钮</button>
  <button @click.middle="alert('你按了鼠标滚轮')">按钮</button>
  <button @click.right="alert('你按了鼠标右击键')">按钮</button>
</div>
```

# v-model

### 注意

**注意一**：`v-model`  会忽略所有表单元素的  `value`、`checked`、`selected`  特性的初始值而总是将 Vue 实例的数据作为数据来源。直接给元素 value 赋值不会生效的，你应该通过 JavaScript 在组件的  `data`  选项中声明初始值。

**注意二**：`v-model`  在内部使用不同的属性为不同的输入元素并抛出不同的事件

- text 和 textarea 元素使用  `value`  属性和  `input`  事件（内部监听 input 事件）
- checkbox 和 radio 使用  `checked`  属性和  `change`  事件（内部监听 change 事件）
- select 字段将  `value`  作为 prop 并将  `change`  作为事件（内部监听 change 事件）

**说明：** change 和 input 区别就是，input 实时更新数据，change 不是实时更新。

## 文本

- 单行文本
  使用  `v-model`  指令，在实例 data 中声明绑定的 message 数据项，即可完成数据双向绑定。

```html
<body>
  <div id="app">
    <input v-model="msg" placeholder="请输入..." />
    <p>输入的是: {{ msg }}</p>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data: {
        msg: "",
      },
    });
  </script>
</body>
```

- 多行文本

```html
<body>
  <div id="app">
    <span>Multiline message is:</span>
    <p style="white-space: pre-line;">{{ message }}</p>
    <br/>
    <textarea v-model="message" placeholder="add multiple lines"></textarea>
  </div>
  <script>
    var vue = new Vue({
      el: "#app",
      data() {
	    return {
		    message: "",
		};
      },
    });
  </script>
</body>
```

## 按钮

checkbox 和 radio 使用  `checked`  属性，当选中时 data 中声明的绑定项的值就为元素的 `value` 值

- 单选按钮
  将单选按钮绑定到同一个 picked，即可完成数据绑定

```html
<body>
  <div id="app">
    <!-- 将单选按钮绑定到同一个 picked -->
    <input type="radio" id="one" value="One" v-model="picked" />
    <label for="one">One</label>
    <br />
    <input type="radio" id="two" value="Two" v-model="picked" />
    <label for="two">Two</label>
    <br />
    <span>Picked: {{ picked }}</span>
  </div>
  <script>
    var vue = new Vue({
      el: "#app",
      data() {
		      return {
			      picked: "",
			};
	    },
    });
  </script>
</body>
```

## 复选框

- 复选框绑定的是一个布尔值：`true` 和 `false`

```html
<body>
  <div id="app">
    <input type="checkbox" id="checkbox" v-model="checked" />
    <label for="checkbox">{{ checked }}</label>
  </div>
  <script>
    // 绑定布尔值
    var vue = new Vue({
      el: "#app",
      data() {
        return {
          checked: false,
        };
      },
    });
  </script>
</body>
```

- 把多个复选框，绑定到同一个数组，方便数据收集，此时数组里的值为`value`中的值

```html
<body>
  <div id="app">
    <input type="checkbox" id="syl1" value="syl1" v-model="checkedNames" />
    <label for="syl1">syl1</label>
    <input type="checkbox" id="syl2" value="syl2" v-model="checkedNames" />
    <label for="syl2">syl2</label>
    <input type="checkbox" id="syl3" value="syl3" v-model="checkedNames" />
    <label for="syl3">syl3</label>
    <br />
    <span>Checked names: {{ checkedNames }}</span>
  </div>
  <script>
    var vue = new Vue({
      el: "#app",
      data() {
        return {
          checkedNames: [],
        };
    },
    });
  </script>
</body>
```

- 在标签中声明  `true-value="yes"`  和  `false-value="no"`  这两个属性，当选中时就是 true-value 属性指定的值，当未选中时就是 false-value 属性值（可设置为空）

```html
<body>
  <div id="app">
    <input
      type="checkbox"
      v-model="toggle"
      true-value="yes"
      false-value="no"
    />
    <p>toggle:{{toggle}}</p>
  </div>
</body>
```

## 选择框

- 在 select 元素上使用  `v-model`  指令，可以绑定当前选中的 option

```html
<div id="app">
  <!-- select 标签是绑定  数据项 selected -->
  <select v-model="selected">
    <option disabled value="">请选择</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>
</div>
```

- 选择框的值绑定，直接指定每个  `option`  的  `value`，可以是固定的，也可以是使用  `v-bind:value`  动态绑定的

```html
<div id="app">
  <!-- 当选中第一个选项时，selected 为字符串 "abc" -->
  <select v-model="selected">
    <!-- 固定赋值value -->
    <option value="abc">ABC</option>
    <!-- 使用 v-bind 绑定值 -->
    <option v-bind:value="optionValue">DEF</option>
  </select>
  <p>{{selected}}</p>
</div>
```

## 修饰符

- `.lazy`  修饰符，可以将抛出事件由 input 改为 change，使表单元素惰性更新，不实时更新。

```html
<body>
  <div id="app">
    <!--使用 .lazy 修饰符将文本框 抛出的事件改为 change 事件，不再实时更新，只有文本框失去焦点才更新数据 惰性更新 -->
    <input v-model.lazy="msg" />
    <p>{{msg}}</p>
  </div>
</body>
```

- `number`  修饰符，自动将用户的输入值转为数值类型，用户即使输入的是非数值类型，也会进行转换，无法转换时，会返回原始的字符串

```html
<div id="app">
  <p>没有使用 .number 修饰符</p>
  <input v-model="number1" type="number" />
  <!-- 使用 typeof 对值类型检测 -->
  <p>{{typeof(number1)}}</p>
  <p>使用 .number 修饰符</p>
  <input v-model.number="number2" type="number" />
  <!-- 使用 typeof 对值类型检测 -->
  <p>{{typeof(number2)}}</p>
</div>
```

- `.trim` 修饰符，表单元素值首尾空格，自动过滤。

```html
<div id="app">
  <input v-model.trim="msg" type="text" />
  <p>首尾空格被过滤了：{{msg}}</p>
</div>
```

# 组件

## 全局组件

`Vue.component()`  方法注册全局组件

- 如果`component`内仅仅传递字符串，则返回该字符串的组件

```html
<body>
  <div id="app">
    <syl></syl>
  </div>
  <script>
    // Vue.component(组件名字,template:{元素标签})
    Vue.component("syl", {
      template: "<h1>实验楼全局组件</h1>",
    });
    var app = new Vue({
      el: "#app",
    });
  </script>
</body>
```

### 数据定义

- `data` 部分必须是一个函数不然会影响其他组件

```html
<script>
  // 注册一个全局可复用组件
  Vue.component("button-counter", {
    data() {
      return {
        counter: 0,
      };
    },
    template: '<button @click="counter++">{{counter}}</button>',
  });
  var app = new Vue({
    el: "#app",
  });
</script>
```

## 局部组件

在定义的 Vue 示例中才能使用的组件，下例为挂载到 `header` 上的组件，仅能在`header` 内部使用

```html
<div id="header">
  <syl-header></syl-header>
</div>
<script>
var header = new Vue({
    el: "#header",
    // 直接将组件内容放在components中
    components: {
      "syl-header": {
        template: "<h2>我是局部组件header，只有我们父级才能调用</h2>",
      },
    },
  });
</script>
```

## 传递数据

### 父组件向子组件传递数据

```html
<body>
  <div id="app">
    <title-component post-title="syl1"></title-component>
    <title-component post-title="syl2"></title-component>
    <title-component post-title="syl3"></title-component>
  </div>
  <script>
    // 注册一个 title 组件，通过传入不同的 title 值，渲染不同的东西
    // 组件上 传递的 props 属性名为 kebab-case（短横线分隔命名）的要转换为驼峰命名
    Vue.component("title-component", {
      props: ["postTitle"], // post-title 转换为驼峰命名
      template: "<p>{{postTitle}}</p>",
    });
    var app = new Vue({
      el: "#app",
    });
  </script>
</body>
```

- 多项数据

```html
<body>
  <div id="app">
    <child-component
      id="1"
      title="hello syl"
      content="you are welcom"
    ></child-component>
  </div>
  <script>
    // 注册一个子组件
    Vue.component("child-component", {
      // props 对象形式，传递属性值 进行类型检测，在脚手架环境中很有用
      props: {
        id: Number,
        title: String,
        content: String,
      },
      // 使用 es6 模板字符串书写格式更优美
      template: "<div><p>id:{{id}}</p><p>title:{{title}}</p><p>content:{{content}}</p></div>",
    });
    var app = new Vue({
      el: "#app",
    });
  </script>
</body>
```

### 子组件向父组件传递数据

子组件向父组件数据传递套路：

第一步：子组件绑定事件。

第二步：子组件绑定事件触发，使用  $emit 创建自定义事件并传入需要传值给父组件的数据。

第三步：在子组件标签上 用 v-on 绑定自定义事件，在父组件中声明自定义事件处理的方法。

第四步：父组件方法，接受自定义事件传的参数，就完成了整个由下到上的数据流。

```html
<body>
  <div id="app">
    <child-component v-on:send-msg="getMsg"></child-component>
  </div>
  <script>
    // 定义一个子组件，template 绑定 click 事件
    // 当 click 事件触发就使用 emit 自定义一个事件 send-msg，传入参数 “我是子组件请求与你通信”
    // $emit('send-msg','我是子组件请求与你通信')
    // 子组件标签上绑定自定义事件 send-msg，并绑定上父级的方法 getMsg，即可完成了子父组件通信
    // <child-component v-on:send-msg="getMsg"></child-component>
    Vue.component("child-component", {
      template: `
              <button v-on:click="$emit('send-msg','我是子组件请求与你通信')">
              Click me
              </button>
              `,
    });
    var app = new Vue({
      el: "#app",
      methods: {
        getMsg: function (msg) {
          // 弹出子组件传递的信息
          alert(msg);
        },
      },
    });
  </script>
</body>
```

### 动态绑定

> 使用 v-bind 动态绑定

```html
<body>
  <div id="app">
    <!-- 使用 v-bind 简写模式 动态绑定 props 值 -->
    <child-component
      :name="name"
      :age="age"
      :height="height"
    ></child-component>
    <child-component
      :name="name+'2'"
      :age="age+1"
      :height="height"
    ></child-component>
  </div>
  <script>
    // 定义一个子组件
    Vue.component("child-component", {
      // 使用属性类型检测
      props: {
        name: String,
        age: Number,
        height: String,
      },
      template: `
          <ul>
              <li>{{name}}</li>
              <li>{{age}}</li>
              <li>{{height}}</li>
          </ul>
          `,
    });
    var app = new Vue({
      el: "#app",
      data() {
        return {
          name: "syl",
          age: 20,
          height: "180cm",
        };
      },
    });
  </script>
</body>
```

# 生命周期

- created 钩子函数内我们可以进行异步数据请求
  [生命周期](https://doc.shiyanlou.com/document-uid940410labid10292timestamp1552640797492.png)

```html
<body>
  <div id="app">
    <button @click="handleClick">{{name}}</button>
  </div>
  <script>
    var app = new Vue({
      el: "#app",
      data() {
        return {
          name: "syl",
        };
      },
      methods: {
        handleClick: function () {
          this.name = "syl syl";
        },
      },
      beforeCreate() {
        alert(
          "在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用"
        );
      },
      created() {
        alert(
          "在实例创建完成后被立即调用,挂载阶段还没开始，$el 属性目前不可见"
        );
      },
      beforeMount() {
        alert("在挂载开始之前被调用：相关的 render 函数首次被调用");
      },
      mounted() {
        alert("el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子");
      },
      beforeUpdate() {
        alert("数据更新时调用");
      },
      updated() {
        alert("组件 DOM 已经更新");
      },
      beforeDestroy() {},
      destroyed() {},
    });
  </script>
</body>
```

## 挂载[[Axios#使用方式|Axios]]

```html
<script>
    var app = new Vue({
        el: "#app",
        data: {
            dataList: [],
        },
        methods: {
            getData() {
                axios.get('1.json')
                    .then(res => {
                        this.dataList = res.data;
                    })
            }
        },
        created() {
            this.getData();
        },
    });
</script>
```
