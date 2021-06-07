# Vue.js 目录结构

## 包目录

|  目录/文件   |                                        说明                                        |
| :----------: | :--------------------------------------------------------------------------------: |
|    build     |                             项目构建(webpack)相关代码                              |
|    config    |                  配置目录，包括端口号等。我们初学可以使用默认的。                  |
| node_modules |                               npm 加载的项目依赖模块                               |
|     src      | 这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件： |
|   assets:    |                             放置一些图片，如 logo 等。                             |
| components:  |                        目录里面放了一个组件文件，可以不用。                        |
|   App.vue:   |        项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。        |
|   main.js:   |                                  项目的核心文件。                                  |
|    static    |                           静态资源目录，如图片、字体等。                           |
|     test     |                                初始测试目录，可删除                                |
|  .xxxx 文件  |                   这些是一些配置文件，包括语法配置，git 配置等。                   |
|  index.html  |               首页入口文件，你可以添加一些 meta 信息或统计代码啥的。               |
| package.json |                                   项目配置文件。                                   |
|  README.md   |                           项目的说明文档，markdown 格式                            |

# Vue.js 模板语法

Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。

Vue.js 的核心是一个允许你采用简洁的模板语法来声明式的将数据渲染进 DOM 的系统。

## 插值

### 文本

数据绑定最常见的形式就是使用 {{...}}（双大括号）的文本插值：

```html
<div id="app">
  <p>{{ message }}</p>
</div>
```

### Html

使用 v-html 指令用于输出 html 代码：

```html
<div id="app">
  <div v-html="message"></div>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: '<h1>百度一下</h1>',
    },
  });
</script>
```

### 属性

HTML 属性中的值应使用 v-bind 指令。

```html
<div id="app">
  <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1" /> <br /><br />
  <div v-bind:class="{'class1': use}">v-bind:class 指令</div>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      use: false,
    },
  });
</script>
```

### 表达式

Vue.js 都提供了完全的 JavaScript 表达式支持。

```html
<div id="app">
  {{5+5}}<br />
  {{ ok ? 'YES' : 'NO' }}<br />
  {{ message.split('').reverse().join('') }}
  <div v-bind:id="'list-' + id">菜鸟教程</div>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      ok: true,
      message: 'RUNOOB',
      id: 1,
    },
  });
</script>
```

## 指令

指令是带有 v- 前缀的特殊属性。

指令用于在表达式的值改变时，将某些行为应用到 DOM 上。

```html
<!-- 这里， v-if 指令将根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素。 -->
<div id="app">
  <p v-if="seen">现在你看到我了</p>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      seen: true,
    },
  });
</script>
```

### 参数

参数在指令后以冒号指明。

```html
<!--  v-bind 指令被用来响应地更新 HTML 属性 -->
<div id="app">
  <pre><a v-bind:href="url">菜鸟教程</a></pre>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      url: 'http://www.runoob.com',
    },
  });
</script>

<!-- v-on 指令，它用于监听 DOM 事件: -->
<a v-on:click="doSomething"></a>
```

### 修饰符

修饰符是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()：

```html
<form v-on:submit.prevent="onSubmit"></form>
```

## 用户输入

数据的双向绑定。

v-model 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

```html
<div id="app">
  <p>{{ message }}</p>
  <input v-model="message" />
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: 'Runoob!',
    },
  });
</script>
```

## 过滤器

Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示, 格式如下：

```html
<!-- 在两个大括号中 -->
{{ message | capitalize }}

<!-- 在 v-bind 指令中 -->
<div v-bind:id="rawId | formatId"></div>
```

过滤器函数接受表达式的值作为第一个参数。

```html
<!-- 以下实例对输入的字符串第一个字母转为大写： -->
<div id="app">{{ message | capitalize }}</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: 'runoob',
    },
    filters: {
      capitalize: function (value) {
        if (!value) return '';
        value = value.toString();
        return value.charAt(0).toUpperCase() + value.slice(1);
      },
    },
  });
</script>
```

```html
<!-- 过滤器可以串联： -->
{{ message | filterA | filterB }}

<!-- 过滤器是 JavaScript 函数，因此可以接受参数： -->
<!-- 这里，message 是第一个参数，字符串 'arg1' 将传给过滤器作为第二个参数， arg2 表达式的值将被求值然后传给过滤器作为第三个参数。 -->
{{ message | filterA('arg1', arg2) }}
```

## 缩写

### v-bind

```html
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

### v-on

```html
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

# Vue.js 条件语句

## 条件判断

### v-if

```html
<div id="app">
  <!-- v-if 将根据 seen 的值（true|false）来决定是否插入 p 元素 -->
  <p v-if="seen">现在你看到我了</p>
  <!-- v-if 将根据 ok 的值（true|false）来决定是否插入 template 元素 -->
  <template v-if="ok">
    <h1>菜鸟教程</h1>
    <p>学的不仅是技术，更是梦想！</p>
    <p>哈哈哈，打字辛苦啊！！！</p>
  </template>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      seen: true,
      ok: true,
    },
  });
</script>
```

### v-else

```html
<!-- 随机生成一个数字，判断是否大于0.5，然后输出对应信息： -->
<div id="app">
  <div v-if="Math.random() > 0.5">Sorry</div>
  <div v-else>Not sorry</div>
</div>

<script>
  new Vue({
    el: '#app',
  });
</script>
```

### v-else-if

v-else-if 在 2.1.0 新增，顾名思义，用作 v-if 的 else-if 块。可以链式的多次使用。

```html
<!-- 判断 type 变量的值： -->
<div id="app">
  <div v-if="type === 'A'">A</div>
  <div v-else-if="type === 'B'">B</div>
  <div v-else-if="type === 'C'">C</div>
  <div v-else>Not A/B/C</div>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      type: 'C',
    },
  });
</script>
```

`v-else 、v-else-if 必须跟在 v-if 或者 v-else-if之后。`

### v-show

也可以使用 v-show 指令来根据条件展示元素。

```html
<h1 v-show="ok">Hello!</h1>
```

## v-if 与 v-show

两者都是控制元素的展示和隐藏，但是 v-if 是通过 display:none; 属性控制的， v-show 则是通过 opacity: 0; 属性控制的；对于不需要经常切换展示和隐藏的元素可以使用 v-if 指令，对于需要经常切换展示和隐藏的元素则使用 v-show 指令。

# Vue.js 循环

循环使用 v-for 指令。

v-for 指令需要以 site in sites 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。

v-for 可以绑定数据到数组来渲染一个列表：

```html
<div id="app">
  <ol>
    <li v-for="site in sites">{{ site.name }}</li>
  </ol>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      sites: [{ name: 'Runoob' }, { name: 'Google' }, { name: 'Taobao' }],
    },
  });
</script>
```

## v-for 迭代对象

```html
<div id="app">
  <ul>
    <li v-for="value in object">{{ value }}</li>
  </ul>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      object: {
        name: '菜鸟教程',
        url: 'http://www.runoob.com',
        slogan: '学的不仅是技术，更是梦想！',
      },
    },
  });
</script>
```

## v-for 参数

```html
<!--（元素） -->
<li v-for="(value) in object">{{ index }}</li>
<!--（元素，键名） -->
<li v-for="(value, key) in object">{{ index }}. {{ key }}</li>
<!--（元素，键名，索引） -->
<li v-for="(value, key, index) in object">{{ index }}. {{ key }} : {{ value }}</li>
```

```html
<div id="app">
  <ul>
    <li v-for="(value, key, index) in object">{{ index }}. {{ key }} : {{ value }}</li>
  </ul>
</div>
```

## v-for 迭代整数

```html
<!-- 循环输出整数 -->
<div id="app">
  <ul>
    <li v-for="n in 10">{{ n }}</li>
  </ul>
</div>
```

# Vue.js 计算属性

计算属性关键词: computed。

计算属性在处理一些复杂逻辑时是很有用的。

```html
<!-- 输出反转字符串 -->
<!-- 例一 -->
<div id="app">{{ message.split('').reverse().join('') }}</div>

<!-- 例二 -->
<div id="app">
  <p>原始字符串: {{ message }}</p>
  <p>计算后反转字符串: {{ reversedMessage }}</p>
</div>

<script>
  var vm = new Vue({
    el: '#app',
    data: {
      message: 'Runoob!',
    },
    computed: {
      // 计算属性的 getter
      reversedMessage: function () {
        // `this` 指向 vm 实例
        return this.message.split('').reverse().join('');
      },
    },
  });
</script>
```

## computed vs methods

当然也可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。

可以说使用 computed 性能会更好，但是如果不希望缓存，可以使用 methods 属性。

```js
methods: {
  reversedMessage2: function () {
    return this.message.split('').reverse().join('')
  }
}
```

## computed setter

computed 属性默认只有 getter ，不过在需要时也可以提供一个 setter ：

```js
var vm = new Vue({
  el: '#app',
  data: {
    name: 'Google',
    url: 'http://www.google.com',
  },
  computed: {
    site: {
      // getter
      get: function () {
        return this.name + ' ' + this.url;
      },
      // setter
      set: function (newValue) {
        var names = newValue.split(' ');
        this.name = names[0];
        this.url = names[names.length - 1];
      },
    },
  },
});
// 调用 setter， vm.name 和 vm.url 也会被对应更新
vm.site = '百度一下 http://www.baidu.com';
document.write('name: ' + vm.name); // name: 百度一下
document.write('<br>');
document.write('url: ' + vm.url); // url: http://www.baidu.com
```

# Vue.js 监听属性

Vue.js 监听属性 watch，可以通过 watch 来响应数据的变化。

```html
<!-- 通过watch实现计数器 -->
<div id="app">
  <p style="font-size:25px;">计数器: {{ counter }}</p>
  <button @click="counter++" style="font-size:25px;">点我</button>
</div>

<script type="text/javascript">
  var vm = new Vue({
    el: '#app',
    data: {
      counter: 1,
    },
  });
  vm.$watch('counter', function (nval, oval) {
    alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
  });
</script>
```

```html
<!-- 千米与米之间的换算 -->
<div id="computed_props">
  千米 : <input type="text" v-model="kilometers" /> 米 : <input type="text" v-model="meters" />
</div>
<p id="info"></p>

<script type="text/javascript">
  var vm = new Vue({
    el: '#computed_props',
    data: {
      kilometers: 0,
      meters: 0,
    },
    methods: {},
    computed: {},
    watch: {
      kilometers: function (val) {
        this.kilometers = val;
        this.meters = this.kilometers * 1000;
      },
      meters: function (val) {
        this.kilometers = val / 1000;
        this.meters = val;
      },
    },
  });
  // $watch 是一个实例方法
  vm.$watch('kilometers', function (newValue, oldValue) {
    // 这个回调将在 vm.kilometers 改变后调用
    document.getElementById('info').innerHTML = '修改前值为: ' + oldValue + '，修改后值为: ' + newValue;
  });
</script>
```

# Vue.js 样式绑定

## Vue.js class

class 与 style 是 HTML 元素的属性，用于设置元素的样式，我们可以用 v-bind 来设置样式属性。

Vue.js v-bind 在处理 class 和 style 时， 专门增强了它。表达式的结果类型除了字符串之外，还可以是对象或数组。

## class 属性绑定

```html
<!-- 1. -->
<div v-bind:class="{ 'active': isActive }"></div>
<!-- 1.实例 -->
<div class="active"></div>

<!-- 2. -->
<div class="static" v-bind:class="{ 'active' : isActive, 'text-danger' : hasError }"></div>
<!-- 2.实例 -->
<div class="static active text-danger"></div>

<!-- 3. -->
<div id="app"><div v-bind:class="classObject"></div></div>
<!-- 3.实例 -->
<div class="static active text-danger"></div>

<!-- 4. -->
<script>
  new Vue({
    el: '#app',
    data: {
      isActive: true,
      error: {
        value: true,
        type: 'fatal',
      },
    },
    computed: {
      classObject: function () {
        return {
          base: true,
          active: this.isActive && !this.error.value,
          'text-danger': this.error.value && this.error.type === 'fatal',
        };
      },
    },
  });
</script>

<!-- 5. -->
<div v-bind:class="[activeClass, errorClass]"></div>

<!-- 4 5.实例 -->
<div class="active text-danger"></div>

<!-- 6. -->
<!-- errorClass 是始终存在的，isActive 为 true 时添加 activeClass 类 -->
<div v-bind:class="[errorClass ,isActive ? activeClass : '']"></div>
```

## Vue.js style(内联样式)

1. v-bind:style 直接设置样式：

```html
<div id="app">
  <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">百度一下</div>
</div>

<!-- 实例 -->
<div style="color: green; font-size: 30px;">百度一下</div>
```

2. 直接绑定到一个样式对象：

```html
<div id="app">
  <div v-bind:style="styleObject">菜鸟教程</div>
</div>
```

3. 通过数组方式绑定多个样式对象：

```html
<div id="app">
  <div v-bind:style="[baseStyles, overridingStyles]">菜鸟教程</div>
</div>
```

# Vue.js 事件注册器

事件监听可以使用 v-on 指令。

## 事件修饰符

Vue.js 为 v-on 提供了事件修饰符来处理 DOM 事件细节，如：event.preventDefault() 或 event.stopPropagation()。

Vue.js 通过由点 . 表示的指令后缀来调用修饰符。

- .stop - 阻止冒泡
- .prevent - 阻止默认事件
- .capture - 阻止捕获
- .self - 只监听触发该元素的事件
- .once - 只触发一次
- .left - 左键事件
- .right - 右键事件
- .middle - 中间滚轮事件

```html
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
<!-- 修饰符可以串联  -->
<a v-on:click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>
<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>

<!-- click 事件只能点击一次，2.1.4版本新增 -->
<a v-on:click.once="doThis"></a>
```

## 按键修饰符

Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：

```html
<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit" />

<!-- 按键修饰符别名 -->
<!-- 同上 -->
<input v-on:keyup.enter="submit" />
<!-- 缩写语法 -->
<input @keyup.enter="submit" />
```

全部按键别名：

- .enter
- .tab
- .delete (捕获 "删除" 和 "退格" 键)
- .esc
- .space
- .up
- .down
- .left
- .right
- .ctrl
- .alt
- .shift
- .meta

```html
<p>
  <!-- Alt + C -->
  <input @keyup.alt.67="clear" />
  <!-- Ctrl + Click -->
</p>

<div @click.ctrl="doSomething">Do something</div>
```

# Vue.js 表单

双向数据绑定流程图：
![20151109171527_549.png](https://i.loli.net/2021/06/01/niSCa1lE267jJeN.png)

## 表单控件

### 输入框

```html
<div id="app">
  <p>input 元素：</p>
  <input v-model="message" placeholder="编辑我……" />
  <p>消息是: {{ message }}</p>

  <p>textarea 元素：</p>
  <p style="white-space: pre">{{ message2 }}</p>
  <textarea v-model="message2" placeholder="多行文本输入……"></textarea>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: 'baidu',
      message2: '百度一下\r\nhttp://www.baidu.com',
    },
  });
</script>
```

### 复选框

复选框如果是一个为逻辑值，如果是多个则绑定到同一个数组：

```html
<div id="app">
  <p>单个复选框：</p>
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">{{ checked }}</label>

  <p>多个复选框：</p>
  <input type="checkbox" id="baidu" value="Baidu" v-model="checkedNames" />
  <label for="baidu">Baidu</label>
  <input type="checkbox" id="google" value="Google" v-model="checkedNames" />
  <label for="google">Google</label>
  <input type="checkbox" id="taobao" value="Taobao" v-model="checkedNames" />
  <label for="taobao">taobao</label>
  <br />
  <span>选择的值为: {{ checkedNames }}</span>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      checked: false,
      checkedNames: [],
    },
  });
</script>
```

### select 列表

```html
<div id="app">
  <select v-model="selected" name="fruit">
    <option value="">选择一个网站</option>
    <option value="www.baidu.com">Baidu</option>
    <option value="www.google.com">Google</option>
  </select>

  <div id="output">选择的网站是: {{selected}}</div>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      selected: '',
    },
  });
</script>
```

## 修饰符

### .lazy

在默认情况下， v-model 在 input 事件中同步输入框的值与数据，但你可以添加一个修饰符 lazy ，从而转变为在 change 事件中同步：

```html
<!-- 在 "change" 而不是 "input" 事件中更新 -->
<input v-model.lazy="msg" />
```

### .number

如果想自动将用户的输入值转为 Number 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个修饰符 number 给 v-model 来处理输入值：

```html
<input v-model.number="age" type="number" />
```

### .trim

如果要自动过滤用户输入的首尾空格，可以添加 trim 修饰符到 v-model 上过滤输入：

```html
<input v-model.trim="msg" />
```

# Vue.js 组件

组件（Component）是 Vue.js 最强大的功能之一。

组件可以扩展 HTML 元素，封装可重用的代码。

组件系统让我们可以用独立可复用的小组件来构建大型应用，几乎任意类型的应用的界面都可以抽象为一个组件树：

![components.png](https://i.loli.net/2021/06/04/aIYgLiFxbjK7JUe.png)

注册一个全局组件语法格式如下：

```html
<!-- 注册一个组件 -->
<script>
  Vue.component(tagName, options); // tagName:组件名；options:配置项
</script>

<!-- 调用组件 -->
<tagName></tagName>
```

### 全局组件

即所有的实例都可以使用的组件：

```html
<div id="app">
  <tagName></tagName>
</div>

<script>
  // 注册
  Vue.component('tagName', {
    template: '<h1>自定义组件!</h1>',
  });
  // 创建根实例
  new Vue({
    el: '#app',
  });
</script>
```

### 局部组件

即在当前的实例中才可以使用的组件：

```html
<div id="app">
  <tagName></tagName>
</div>

<script>
  var Child = {
    template: '<h1>自定义组件!</h1>',
  };

  // 创建根实例
  new Vue({
    el: '#app',
    components: {
      // <tagName> 将只在父模板可用
      tagName: Child,
    },
  });
</script>
```

## Prop

prop 是子组件用来接受父组件传递过来的数据的一个自定义属性。

父组件的数据需要通过 props 把数据传给子组件，子组件需要显式地用 props 选项声明 "prop"：

`注意: prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是不会反过来。`

```html
<div id="app">
  <child message="hello!"></child>
</div>

<script>
  // 注册
  Vue.component('child', {
    // 声明 props
    props: ['message'],
    // 同样也可以在 vm 实例中像 "this.message" 这样使用
    template: '<span>{{ message }}</span>',
  });
  // 创建根实例
  new Vue({
    el: '#app',
  });
</script>
```

### 动态 Prop

类似于用 v-bind 绑定 HTML 特性到一个表达式，也可以用 v-bind 动态绑定 props 的值到父组件的数据中。每当父组件的数据变化时，该变化也会传导给子组件：

```html
<div id="app">
  <div>
    <input v-model="parentMsg" />
    <br />
    <child v-bind:message="parentMsg"></child>
  </div>
</div>

<script>
  // 注册
  Vue.component('child', {
    // 声明 props
    props: ['message'],
    // 同样也可以在 vm 实例中像 "this.message" 这样使用
    template: '<span>{{ message }}</span>',
  });
  // 创建根实例
  new Vue({
    el: '#app',
    data: {
      parentMsg: '父组件内容',
    },
  });
</script>
```

### Props 验证

组件可以为 props 指定验证要求。

为了定制 prop 的验证方式，可以为 props 中的值提供一个带有验证需求的对象，而不是一个字符串数组。

```js
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true,
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100,
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' };
      },
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1;
      },
    },
  },
});
```

当 prop 验证失败的时候，(开发环境构建版本的) Vue 将会产生一个控制台的警告。

type 可以是下面原生构造器：

- String
- Number
- Boolean
- Array
- Object
- Date
- Function
- Symbol

type 也可以是一个自定义构造器，使用 instanceof 检测。

# Vue.js 组件 - 自定义事件

父组件是使用 props 传递数据给子组件，但如果子组件要把数据传递回去，就需要使用自定义事件！

我们可以使用 v-on 绑定自定义事件, 每个 Vue 实例都实现了事件接口(Events interface)，即：

- 使用 $on(eventName) 监听事件
- 使用 $emit(eventName) 触发事件

另外，父组件可以在使用子组件的地方直接用 v-on 来监听子组件触发的事件。

```html
<div id="app">
  <div id="counter-event-example">
    <p>{{ total }}</p>
    <button-counter v-on:increment="incrementTotal"></button-counter>
    <button-counter v-on:increment="incrementTotal"></button-counter>
  </div>
</div>

<script>
  Vue.component('button-counter', {
    template: '<button v-on:click="incrementHandler">{{ counter }}</button>',
    data: function () {
      return {
        counter: 0,
      };
    },
    methods: {
      incrementHandler: function () {
        this.counter += 1;
        this.$emit('increment');
      },
    },
  });
  new Vue({
    el: '#counter-event-example',
    data: {
      total: 0,
    },
    methods: {
      incrementTotal: function () {
        this.total += 1;
      },
    },
  });
</script>
```

如果想在某个组件的根元素上监听一个原生事件。可以使用 .native 修饰 v-on 。

```html
<my-component v-on:click.native="doTheThing"></my-component>
```

### data 必须是一个函数

这样的好处就是每个实例可以维护一份被返回对象的独立的拷贝，如果 data 是一个对象则会影响到其他实例。

```js
data: function () {
  return {
    count: 0
  }
}
```

```html
<div id="components-demo3" class="demo">
  <button-counter2></button-counter2>
  <button-counter2></button-counter2>
  <button-counter2></button-counter2>
</div>

<script>
  var buttonCounter2Data = {
    count: 0,
  };
  Vue.component('button-counter2', {
    /*
    data: function () {
        // data 选项是一个函数，组件不相互影响
        return {
            count: 0
        }
    },
    */
    data: function () {
      // data 选项是一个对象，会影响到其他实例
      return buttonCounter2Data;
    },
    template: '<button v-on:click="count++">点击了 {{ count }} 次。</button>',
  });
  new Vue({ el: '#components-demo3' });
</script>
```

## 自定义组件的 v-model

组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件。

```html
<input v-model="parentData" />

<!-- 等价于 -->
<input :value="parentData" @input="parentData = $event.target.value" />
```

```html
<div id="app">
  <runoob-input v-model="num"></runoob-input>
  <p>输入的数字为:{{num}}</p>
</div>
<script>
  Vue.component('runoob-input', {
    template: `
    <p>   <!-- 包含了名为 input 的事件 -->
      <input
       ref="input"
       :value="value" 
       @input="$emit('input', $event.target.value)"
      >
    </p>
    `,
    props: ['value'], // 名为 value 的 prop
  });

  new Vue({
    el: '#app',
    data: {
      num: 100,
    },
  });
</script>
```

由于 v-model 默认传的是 value，不是 checked，所以对于复选框或者单选框的组件时，需要使用 model 选项，model 选项可以指定当前的事件类型和传入的 props。

```html
<!-- 实例中 lovingVue 的值会传给 checked 的 prop，同时当 <base-checkbox> 触发 change 事件时， lovingVue 的值也会更新。 -->
<div id="app">
  <base-checkbox v-model="lovingVue"></base-checkbox>
  <div v-show="lovingVue">如果选择框打勾我就会显示。</div>
</div>
<script>
  // 注册
  Vue.component('base-checkbox', {
    model: {
      prop: 'checked',
      event: 'change', // onchange 事件
    },
    props: {
      checked: Boolean,
    },

    template: `
    <input
      type="checkbox"
      v-bind:checked="checked"
      v-on:change="$emit('change', $event.target.checked)"
    >
  `,
  });
  // 创建根实例
  new Vue({
    el: '#app',
    data: {
      lovingVue: true,
    },
  });
</script>
```

# Vue.js 自定义指令

除了默认设置的核心指令( v-model 和 v-show ), Vue 也允许注册自定义指令。

```html
<!-- 页面载入时，input 元素自动获取焦点 -->
<div id="app">
  <p>页面载入时，input 元素自动获取焦点：</p>
  <input v-focus />
</div>

<script>
  // 注册一个全局自定义指令 v-focus
  Vue.directive('focus', {
    // 当绑定元素插入到 DOM 中。
    inserted: function (el) {
      // 聚焦元素
      el.focus();
    },
  });
  // 创建根实例
  new Vue({
    el: '#app',
  });
</script>
```

## 局部注册指令

```html
<div id="app">
  <p>页面载入时，input 元素自动获取焦点：</p>
  <input v-focus />
</div>

<script>
  // 创建根实例
  new Vue({
    el: '#app',
    directives: {
      // 注册一个局部的自定义指令 v-focus
      focus: {
        // 指令的定义
        inserted: function (el) {
          // 聚焦元素
          el.focus();
        },
      },
    },
  });
</script>
```

## 钩子

### 钩子函数

指令定义函数提供了几个钩子函数（可选）：

- bind: 只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作。
- inserted: 被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于 document 中）。
- update: 被绑定元素所在的模板更新时调用，而不论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新（详细的钩子函数参数见下）。
- componentUpdated: 被绑定元素所在模板完成一次更新周期时调用。
- unbind: 只调用一次， 指令与元素解绑时调用。

### 钩子参数

- el: 指令所绑定的元素，可以用来直接操作 DOM 。
- binding: 一个对象，包含以下属性：
  - name: 指令名，不包括 v- 前缀。
  - value: 指令的绑定值， 例如： v-my-directive="1 + 1", value 的值是 2。
  - oldValue: 指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
  - expression: 绑定值的表达式或变量名。 例如 v-my-directive="1 + 1" ， expression 的值是 "1 + 1"。
  - arg: 传给指令的参数。例如 v-my-directive:foo， arg 的值是 "foo"。
  - modifiers: 一个包含修饰符的对象。 例如： v-my-directive.foo.bar, 修饰符对象 modifiers 的值是 { foo: true, bar: true }。
- vnode: Vue 编译生成的虚拟节点。
- oldVnode: 上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。

```html
<div id="app" v-baidu:hello.a.b="message"></div>

<script>
  Vue.directive('baidu', {
    bind: function (el, binding, vnode) {
      var s = JSON.stringify;
      el.innerHTML =
        'name: ' +
        s(binding.name) +
        '<br>' + // name: "baidu"
        'value: ' +
        s(binding.value) +
        '<br>' + // value: "百度一下!"
        'expression: ' +
        s(binding.expression) +
        '<br>' + // expression: "message"
        'argument: ' +
        s(binding.arg) +
        '<br>' + // argument: "hello"
        'modifiers: ' +
        s(binding.modifiers) +
        '<br>' + // modifiers: {"a":true,"b":true}
        'vnode keys: ' +
        Object.keys(vnode).join(', '); // vnode keys: tag, data, children, text, elm, ns, context, functionalContext, key, componentOptions, componentInstance, parent, raw, isStatic, isRootInsert, isComment, isCloned, isOnce
    },
  });
  new Vue({
    el: '#app',
    data: {
      message: '百度一下!',
    },
  });
</script>
```

当不需要其它的钩子函数的时候，可以简写：

```js
Vue.directive('runoob', function (el, binding) {
  // 设置指令的背景颜色
  el.style.backgroundColor = binding.value.color;
});
```

指令函数可接受所有合法的 JavaScript 表达式，以下实例传入了 JavaScript 对象：

```html
<div id="app">
  <div v-runoob="{ color: 'green', text: '菜鸟教程!' }"></div>
</div>

<script>
  Vue.directive('runoob', function (el, binding) {
    // 简写方式设置文本及背景颜色
    el.innerHTML = binding.value.text;
    el.style.backgroundColor = binding.value.color;
  });
  new Vue({
    el: '#app',
  });
</script>
```

# Vue.js 路由

Vue.js 路由允许我们通过不同的 URL 访问不同的内容。

通过 Vue.js 可以实现多视图的单页 Web 应用（single page web application，SPA）。

Vue.js 路由需要载入 vue-router 库。

## 简单实例

Vue.js + vue-router 可以很简单的实现单页应用。

`<router-link>` 是一个组件，该组件用于设置一个导航链接，切换不同 HTML 内容。 to 属性为目标地址， 即要显示的内容。

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>

<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
</div>

<script>
  // 0. 如果使用模块化机制编程，导入 Vue 和 VueRouter，要调用 Vue.use(VueRouter)

  // 1. 定义（路由）组件。
  // 可以从其他文件 import 进来
  const Foo = { template: '<div>foo</div>' };
  const Bar = { template: '<div>bar</div>' };

  // 2. 定义路由
  // 每个路由应该映射一个组件。 其中"component" 可以是
  // 通过 Vue.extend() 创建的组件构造器，
  // 或者，只是一个组件配置对象。
  // 晚点再讨论嵌套路由。
  const routes = [
    { path: '/foo', component: Foo },
    { path: '/bar', component: Bar },
  ];

  // 3. 创建 router 实例，然后传 `routes` 配置
  // 你还可以传别的配置参数, 不过先这么简单着吧。
  const router = new VueRouter({
    routes, // （缩写）相当于 routes: routes
  });

  // 4. 创建和挂载根实例。
  // 记得要通过 router 配置参数注入路由，
  // 从而让整个应用都有路由功能
  const app = new Vue({
    router,
  }).$mount('#app');

  // 现在，应用已经启动了！
</script>
```

点击过的导航链接都会加上样式 `class ="router-link-exact-active router-link-active"`。

## `<router-link>` 相关属性

### to

表示目标路由的链接。 当被点击后，内部会立刻把 to 的值传到 router.push()，所以这个值可以是一个字符串或者是描述目标位置的对象。

```html
<!-- 字符串 -->
<router-link to="home">Home</router-link>
<!-- 渲染结果 -->
<a href="home">Home</a>

<!-- 使用 v-bind 的 JS 表达式 -->
<router-link v-bind:to="'home'">Home</router-link>

<!-- 不写 v-bind 也可以，就像绑定别的属性一样 -->
<router-link :to="'home'">Home</router-link>

<!-- 同上 -->
<router-link :to="{ path: 'home' }">Home</router-link>

<!-- 命名的路由 -->
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

<!-- 带查询参数，下面的结果为 /register?plan=private -->
<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>
```

### replace

设置 replace 属性的话，当点击时，会调用 router.replace() 而不是 router.push()，导航后不会留下 history 记录。

```html
<router-link :to="{ path: '/abc'}" replace></router-link>
```

### append

设置 append 属性后，则在当前 (相对) 路径前添加其路径。例如，我们从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b

```html
<router-link :to="{ path: 'relative/path'}" append></router-link>
```

### tag

有时候想要 `<router-link>` 渲染成某种标签，例如 `<li>`。 于是使用 tag prop 类指定何种标签，同样它还是会监听点击，触发导航。

```html
<router-link to="/foo" tag="li">foo</router-link>
<!-- 渲染结果 -->
<li>foo</li>
```

### active-class

设置 链接激活时使用的 CSS 类名。可以通过以下代码来替代。

```html
<style>
  ._active {
    background-color: red;
  }
</style>
<p>
  <router-link v-bind:to="{ path: '/route1'}" active-class="_active">Router Link 1</router-link>
  <router-link v-bind:to="{ path: '/route2'}" tag="span">Router Link 2</router-link>
</p>
```

### exact-active-class

配置当链接被精确匹配的时候应该激活的 class。

```html
<p>
  <router-link v-bind:to="{ path: '/route1'}" exact-active-class="_active">Router Link 1</router-link>
  <router-link v-bind:to="{ path: '/route2'}" tag="span">Router Link 2</router-link>
</p>
```

### event

声明可以用来触发导航的事件。可以是一个字符串或是一个包含字符串的数组。

```html
<router-link v-bind:to="{ path: '/route1'}" event="mouseover">Router Link 1</router-link>
```

# Vue.js 过渡 & 动画

## 过渡

Vue 在插入、更新或者移除 DOM 时，提供多种不同方式的应用过渡效果。

Vue 提供了内置的过渡封装组件，该组件用于包裹要实现过渡效果的组件。

### 语法格式

```html
<transition name="nameoftransition">
  <div></div>
</transition>
```

```html
<style>
  /* 可以设置不同的进入和离开动画 */
  /* 设置持续时间和动画函数 */
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 2s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active, 2.1.8 版本以下 */ {
    opacity: 0;
  }
</style>

<div id="databinding">
  <button v-on:click="show = !show">点我</button>
  <transition name="fade">
    <p v-show="show" v-bind:style="styleobj">动画实例</p>
  </transition>
</div>

<script type="text/javascript">
  var vm = new Vue({
    el: '#databinding',
    data: {
      show: true,
      styleobj: {
        fontSize: '30px',
        color: 'red',
      },
    },
    methods: {},
  });
</script>
```

过渡其实就是一个淡入淡出的效果。Vue 在元素显示与隐藏的过渡中，提供了 6 个 class 来切换：

- v-enter：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
- v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
- v-enter-to: 2.1.8 版及以上 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。
- v-leave: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
- v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
- v-leave-to: 2.1.8 版及以上 定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。

![transition.png](https://i.loli.net/2021/06/04/KSBONjcxmETM2rA.png)

==对于这些在过渡中切换的类名来说，如果你使用一个没有名字的 `<transition>`，则 v- 是这些类名的默认前缀。如果你使用了 `<transition name="my-transition">`，那么 v-enter 会替换为 my-transition-enter。==

==v-enter-active 和 v-leave-active 可以控制进入/离开过渡的不同的缓和曲线。==

### css 过渡

```html
<style>
  /* 可以设置不同的进入和离开动画 */
  /* 设置持续时间和动画函数 */
  .slide-fade-enter-active {
    transition: all 0.3s ease;
  }
  .slide-fade-leave-active {
    transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
  }
  .slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active 用于 2.1.8 以下版本 */ {
    transform: translateX(10px);
    opacity: 0;
  }
</style>

<div id="databinding">
  <button v-on:click="show = !show">点我</button>
  <transition name="slide-fade">
    <p v-if="show">测试</p>
  </transition>
</div>

<script type="text/javascript">
  new Vue({
    el: '#databinding',
    data: {
      show: true,
    },
  });
</script>
```

### css 动画

CSS 动画用法类似 CSS 过渡，但是在动画中 v-enter 类名在节点插入 DOM 后不会立即删除，而是在 animationend 事件触发时删除。

```html
<style>
  .bounce-enter-active {
    animation: bounce-in 0.5s;
  }
  .bounce-leave-active {
    animation: bounce-in 0.5s reverse;
  }
  @keyframes bounce-in {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.5);
    }
    100% {
      transform: scale(1);
    }
  }
</style>

<div id="databinding">
  <button v-on:click="show = !show">点我</button>
  <transition name="bounce">
    <p v-if="show">测试</p>
  </transition>
</div>

<script type="text/javascript">
  new Vue({
    el: '#databinding',
    data: {
      show: true,
    },
  });
</script>
```

### 自定义过渡类名

可以通过以下特性来自定义过渡类名：

- enter-class
- enter-active-class
- enter-to-class (2.1.8+)
- leave-class
- leave-active-class
- leave-to-class (2.1.8+)

自定义过渡的类名优先级高于普通的类名，这样就能很好的与第三方（如：animate.css）的动画库结合使用。

```html
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<link href="https://cdn.jsdelivr.net/npm/animate.css@3.5.1" rel="stylesheet" type="text/css" />

<div id="databinding">
  <button v-on:click="show = !show">点我</button>
  <transition
    name="custom-classes-transition"
    enter-active-class="animated tada"
    leave-active-class="animated bounceOutRight"
  >
    <p v-if="show">测试</p>
  </transition>
</div>

<script type="text/javascript">
  new Vue({
    el: '#databinding',
    data: {
      show: true,
    },
  });
</script>
```

### 同时使用过渡和动画

Vue 为了知道过渡的完成，必须设置相应的事件监听器。它可以是 transitionend 或 animationend ，这取决于给元素应用的 CSS 规则。如果使用其中任何一种，Vue 能自动识别类型并设置监听。

但是，在一些场景中，需要给同一个元素同时设置两种过渡动效，比如 animation 很快的被触发并完成了，而 transition 效果还没结束。在这种情况中，就需要使用 type 特性并设置 animation 或 transition 来明确声明需要 Vue 监听的类型。

### 显性的过渡持续时间

Vue 会等待其在过渡效果的根元素的第一个 transitionend 或 animationend 事件。

```html
<!-- 设置一个显性的过渡持续时间（毫秒） -->
<transition :duration="1000">...</transition>

<!-- 设置进入和移出的持续时间（毫秒） -->
<transition :duration="{ enter: 500, leave: 800 }">...</transition>
```

## JavaScript 钩子

可以在属性中声明 JavaScript 钩子:

```html
<transition
  v-on:before-enter="beforeEnter"
  v-on:enter="enter"
  v-on:after-enter="afterEnter"
  v-on:enter-cancelled="enterCancelled"
  v-on:before-leave="beforeLeave"
  v-on:leave="leave"
  v-on:after-leave="afterLeave"
  v-on:leave-cancelled="leaveCancelled"
>
  <!-- ... -->
</transition>

<script>
  // ...
  methods: {
    // --------
    // 进入中
    // --------

    beforeEnter: function (el) {
      // ...
    },
    // 此回调函数是可选项的设置
    // 与 CSS 结合时使用
    enter: function (el, done) {
      // ...
      done()
    },
    afterEnter: function (el) {
      // ...
    },
    enterCancelled: function (el) {
      // ...
    },

    // --------
    // 离开时
    // --------

    beforeLeave: function (el) {
      // ...
    },
    // 此回调函数是可选项的设置
    // 与 CSS 结合时使用
    leave: function (el, done) {
      // ...
      done()
    },
    afterLeave: function (el) {
      // ...
    },
    // leaveCancelled 只用于 v-show 中
    leaveCancelled: function (el) {
      // ...
    }
  }
</script>
```

这些钩子函数可以结合 CSS transitions/animations 使用，也可以单独使用。

当只用 JavaScript 过渡的时候，`在 enter 和 leave 中必须使用 done 进行回调`。否则，它们将被同步调用，过渡会立即完成。

推荐对于仅使用 JavaScript 过渡的元素添加 v-bind:css="false"，Vue 会跳过 CSS 的检测。这也可以避免过渡过程中 CSS 的影响。

```html
<!-- velocity.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/velocity/1.2.3/velocity.min.js"></script>

<div id="databinding">
  <button v-on:click="show = !show">点我</button>
  <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
    <p v-if="show">测试</p>
  </transition>
</div>

<script type="text/javascript">
  new Vue({
    el: '#databinding',
    data: {
      show: false,
    },
    methods: {
      beforeEnter: function (el) {
        el.style.opacity = 0;
        el.style.transformOrigin = 'left';
      },
      enter: function (el, done) {
        Velocity(el, { opacity: 1, fontSize: '1.4em' }, { duration: 300 });
        Velocity(el, { fontSize: '1em' }, { complete: done });
      },
      leave: function (el, done) {
        Velocity(el, { translateX: '15px', rotateZ: '50deg' }, { duration: 600 });
        Velocity(el, { rotateZ: '100deg' }, { loop: 2 });
        Velocity(
          el,
          {
            rotateZ: '45deg',
            translateY: '30px',
            translateX: '30px',
            opacity: 0,
          },
          { complete: done }
        );
      },
    },
  });
</script>
```

## 初始渲染的过渡

可以通过 appear 特性设置节点在初始渲染的过渡。

```html
<transition appear>
  <!-- ... -->
</transition>

<!-- 这里默认和进入/离开过渡一样 -->

<!-- 自定义CSS过渡类名 -->
<transition
  appear
  appear-class="custom-appear-class"
  appear-to-class="custom-appear-to-class"
  (2.1.8+)
  appear-active-class="custom-appear-active-class"
>
  <!-- ... -->
</transition>

<!-- 自定义JavaScript钩子 -->
<transition
  appear
  v-on:before-appear="customBeforeAppearHook"
  v-on:appear="customAppearHook"
  v-on:after-appear="customAfterAppearHook"
  v-on:appear-cancelled="customAppearCancelledHook"
>
  <!-- ... -->
</transition>
```

### 多个元素的过渡

可以设置多个元素的过渡，一般列表与描述：

需要注意的是当有相同标签名的元素切换时，需要`通过 key 特性设置唯一`的值来标记以让 Vue 区分它们，否则 Vue 为了效率只会替换相同标签内部的内容。

```html
<transition>
  <button v-if="docState === 'saved'" key="saved">Edit</button>
  <button v-if="docState === 'edited'" key="edited">Save</button>
  <button v-if="docState === 'editing'" key="editing">Cancel</button>
</transition>

<!-- 重写 -->
<transition>
  <button v-bind:key="docState">{{ buttonMessage }}</button>
</transition>
<script>
    // ...
  computed: {
    buttonMessage: function () {
      switch (this.docState) {
        case 'saved': return 'Edit'
        case 'edited': return 'Save'
        case 'editing': return 'Cancel'
      }
    }
  }
</script>
```

# Vue.js 混入

混入 (mixins)定义了一部分可复用的方法或者计算属性。混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被混入该组件本身的选项。

```js
var vm = new Vue({
  el: '#databinding',
  data: {},
  methods: {},
});
// 定义一个混入对象
var myMixin = {
  created: function () {
    this.startmixin();
  },
  methods: {
    startmixin: function () {
      document.write('欢迎来到混入实例');
    },
  },
};
var Component = Vue.extend({
  mixins: [myMixin],
});
var component = new Component();
```

## 选项合并

当组件和混入对象含有同名选项时，这些选项将以恰当的方式混合。

比如，数据对象在内部会进行浅合并 (一层属性深度)，在和组件的数据发生冲突时以组件数据优先。

```js
var mixin = {
  created: function () {
    document.write('混入调用' + '<br>');
  },
};
new Vue({
  mixins: [mixin],
  created: function () {
    document.write('组件调用' + '<br>');
  },
});

// => 混合调用
// => 组件调用
```

如果 `methods 选项中有相同的函数名`，则 Vue 实例优先级会较高。如下实例，Vue 实例与混入对象的 methods 选项都包含了相同的函数：

```js
var mixin = {
  methods: {
    hellworld: function () {
      document.write('HelloWorld 方法' + '<br>');
    },
    samemethod: function () {
      document.write('Mixin：相同方法名' + '<br>');
    },
  },
};
var vm = new Vue({
  mixins: [mixin],
  methods: {
    start: function () {
      document.write('start 方法' + '<br>');
    },
    samemethod: function () {
      document.write('Main：相同方法名' + '<br>');
    },
  },
});
vm.hellworld(); // => HelloWorld 方法
vm.start(); // => start 方法
vm.samemethod(); // => Main：相同方法名
```

## 全局混入

也可以全局注册混入对象。注意使用！ 一旦使用全局混入对象，将会影响到 所有 之后创建的 Vue 实例。使用恰当时，可以为自定义对象注入处理逻辑。

```js
// 为自定义的选项 'myOption' 注入一个处理器。
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption;
    if (myOption) {
      console.log(myOption);
    }
  },
});

new Vue({
  myOption: 'hello!',
});
// => "hello!"
```

# Vue.js Ajax(axios)

Axios 是一个基于 Promise 的 HTTP 库，可以用在浏览器和 node.js 中。

## GET 方法

```js
new Vue({
  el: '#app',
  data() {
    return {
      info: null,
    };
  },
  mounted() {
    axios
      .get('https://www.runoob.com/try/ajax/json_demo.json')
      .then((response) => (this.info = response))
      .catch((error) => console.log(error));
  },
});
```

### 参数传递

```js
// 直接在 URL 上添加参数 ID=12345
axios
  .get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 也可以通过 params 设置参数：
axios
  .get('/user', {
    params: {
      ID: 12345,
    },
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

## POST 方法

```js
new Vue({
  el: '#app',
  data() {
    return {
      info: null,
    };
  },
  mounted() {
    axios
      .post('https://www.runoob.com/try/ajax/demo_axios_post.php')
      .then((response) => (this.info = response))
      .catch((error) => console.log(error));
  },
});
```

### 参数传递

```js
axios
  .post('/user', {
    firstName: 'Fred', // 参数 firstName
    lastName: 'Flintstone', // 参数 lastName
  })
  .then((response) => console.log(response))
  .catch((error) => console.log(error));
```

## 执行多个并发请求

```js
function getUserAccount() {
  return axios.get('/user/12345');
}
function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}
axios.all([getUserAccount(), getUserPermissions()]).then(
  axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
  })
);
```

## axios API

可以通过向 axios 传递相关配置来创建请求。

```js
axios(config)
// 发送 POST 请求
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
//  GET 请求远程图片
axios({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  responseType:'stream'
})
  .then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});
axios(url[, config])
// 发送 GET 请求（默认的方法）
axios('/user/12345');
```

### 请求方法的别名

为方便使用，官方为所有支持的请求方法提供了别名，可以直接使用别名来发起请求：

注意：在使用别名方法时， url、method、data 这些属性都不必在配置中指定。

```js
axios.request(config)
axios.get(url[, config])
axios.delete(url[, config])
axios.head(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])
```

### 并发

处理并发请求的助手函数：

```js
axios.all(iterable);
axios.spread(callback);
```

### 创建实例

可以使用自定义配置新建一个 axios 实例：

```js
axios.create([config]);
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: { 'X-Custom-Header': 'foobar' },
});
```

### 实例方法

```js
axios#request(config)
axios#get(url[, config])
axios#delete(url[, config])
axios#head(url[, config])
axios#post(url[, data[, config]])
axios#put(url[, data[, config]])
axios#patch(url[, data[, config]])
```

### 请求配置项

下面是创建请求时可用的配置选项，注意只有 url 是必需的。如果没有指定 method，请求将默认使用 get 方法。

```js
{
  // `url` 是用于请求的服务器 URL
  url: "/user",

  // `method` 是创建请求时使用的方法
  method: "get", // 默认是 get

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: "https://some-domain.com/api/",

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 "PUT", "POST" 和 "PATCH" 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data) {
    // 对 data 进行任意转换处理

    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理

    return data;
  }],

  // `headers` 是即将被发送的自定义请求头
  headers: {"X-Requested-With": "XMLHttpRequest"},

  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 12345
  },

  // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: "brackets"})
  },

  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 "PUT", "POST", 和 "PATCH"
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: "Fred"
  },

  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求花费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,

  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // 默认的

  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },

  // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: "janedoe",
    password: "s00pers3cret"
  },

  // `responseType` 表示服务器响应的数据类型，可以是 "arraybuffer", "blob", "document", "json", "text", "stream"
  responseType: "json", // 默认的

  // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: "XSRF-TOKEN", // default

  // `xsrfHeaderName` 是承载 xsrf token 的值的 HTTP 头的名称
  xsrfHeaderName: "X-XSRF-TOKEN", // 默认的

  // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

  // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,

  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status &gt;= 200 &amp;&amp; status &lt; 300; // 默认的
  },

  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // 默认的

  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // "proxy" 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: "127.0.0.1",
    port: 9000,
    auth: : {
      username: "mikeymike",
      password: "rapunz3l"
    }
  },

  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
```

### 响应结构

axios 请求的响应包含以下信息：

```js
{
  // `data` 由服务器提供的响应
  data: {},

  // `status`  HTTP 状态码
  status: 200,

  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: "OK",

  // `headers` 服务器响应的头
  headers: {},

  // `config` 是为请求提供的配置信息
  config: {}
}
```

使用 then 时，会接收下面这样的响应：

```js
axios.get('/user/12345').then(function (response) {
  console.log(response.data);
  console.log(response.status);
  console.log(response.statusText);
  console.log(response.headers);
  console.log(response.config);
});
```

在使用 catch 时，或传递 rejection callback 作为 then 的第二个参数时，响应可以通过 error 对象可被使用。

### 配置默认值

你可以指定将被用在各个请求的配置默认值。

- 全局的 axios 默认值：

```js
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

- 自定义实例默认值：

```js
// 创建实例时设置配置的默认值
var instance = axios.create({
  baseURL: 'https://api.example.com',
});

// 在实例已创建后修改默认值
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
```

### 配置的优先顺序

配置会以一个优先顺序进行合并。这个顺序是：在 lib/defaults.js 找到的库的默认值，然后是实例的 defaults 属性，最后是请求的 config 参数。后者将优先于前者。

```js
// 使用由库提供的配置的默认值来创建实例
// 此时超时配置的默认值是 `0`
var instance = axios.create();

// 覆写库的超时默认值
// 现在，在超时前，所有请求都会等待 2.5 秒
instance.defaults.timeout = 2500;

// 为已知需要花费很长时间的请求覆写超时设置
instance.get('/longRequest', {
  timeout: 5000,
});
```

### 拦截器

在请求或响应被 then 或 catch 处理前拦截它们。

```js
// 添加请求拦截器
axios.interceptors.request.use(
  function (config) {
    // 在发送请求之前做些什么
    return config;
  },
  function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  }
);

// 添加响应拦截器
axios.interceptors.response.use(
  function (response) {
    // 对响应数据做点什么
    return response;
  },
  function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  }
);
```

```js
// 在稍后移除拦截器
var myInterceptor = axios.interceptors.request.use(function () {
  /*...*/
});
axios.interceptors.request.eject(myInterceptor);

// 自定义拦截器
var instance = axios.create();
instance.interceptors.request.use(function () {
  /*...*/
});

// 错误处理
axios.get('/user/12345').catch(function (error) {
  if (error.response) {
    // 请求已发出，但服务器响应的状态码不在 2xx 范围内
    console.log(error.response.data);
    console.log(error.response.status);
    console.log(error.response.headers);
  } else {
    // Something happened in setting up the request that triggered an Error
    console.log('Error', error.message);
  }
  console.log(error.config);
});

// 使用 validateStatus 配置选项定义一个自定义 HTTP 状态码的错误范围
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // 状态码在大于或等于500时才会 reject
  },
});
```

### 取消

使用 cancel token 取消请求。

Axios 的 cancel token API 基于 cancelable promises proposal

可以使用 CancelToken.source 工厂方法创建 cancel token

```js
var CancelToken = axios.CancelToken;
var source = CancelToken.source();

axios
  .get('/user/12345', {
    cancelToken: source.token,
  })
  .catch(function (thrown) {
    if (axios.isCancel(thrown)) {
      console.log('Request canceled', thrown.message);
    } else {
      // 处理错误
    }
  });

// 取消请求（message 参数是可选的）
source.cancel('Operation canceled by the user.');
```

还可以通过传递一个 executor 函数到 CancelToken 的构造函数来创建 cancel token：

注意：可以使用同一个 cancel token 取消多个请求。

```js
var CancelToken = axios.CancelToken;
var cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  }),
});

// 取消请求
cancel();
```

### 请求时使用 application/x-www-form-urlencoded

axios 会默认序列化 JavaScript 对象为 JSON。 如果想使用 application/x-www-form-urlencoded 格式，可以使用下面的配置。

在浏览器环境，可以使用 URLSearchParams API：

```js
const params = new URLSearchParams();
params.append('param1', 'value1');
params.append('param2', 'value2');
axios.post('/foo', params);
```

URLSearchParams 不是所有的浏览器均支持。此外，可以使用 qs 库来编码数据。

```js
const qs = require('qs');
axios.post('/foo', qs.stringify({ bar: 123 }));

// Or in another way (ES6),

import qs from 'qs';
const data = { bar: 123 };
const options = {
  method: 'POST',
  headers: { 'content-type': 'application/x-www-form-urlencoded' },
  data: qs.stringify(data),
  url,
};
axios(options);
```

### Node.js 环境

在 node.js 里, 可以使用 querystring 模块:

```js
const querystring = require('querystring');
axios.post('http://something.com/', querystring.stringify({ foo: 'bar' }));
```

### Promises

axios 依赖原生的 ES6 Promise 实现而被支持。

如果环境不支持 ES6 Promise，你可以使用 polyfill。

### TypeScript 支持

axios 包含 TypeScript 的定义。

```js
import axios from 'axios';
axios.get('/user?ID=12345');
```

# Vue.js Ajax(vue-resource)

Vue 要实现异步加载需要使用到 vue-resource 库。

## Get 请求

```js
// 请求一个txt文本
window.onload = function () {
  var vm = new Vue({
    el: '#box',
    data: {
      msg: 'Hello World!',
    },
    methods: {
      get: function () {
        //发送get请求
        this.$http.get('/try/ajax/ajax_info.txt').then(
          function (res) {
            document.write(res.body);
          },
          function () {
            console.log('请求失败处理');
          }
        );
      },
    },
  });
};
```

如果需要传递数据，可以使用 this.$http.get('get.php',{params : jsonData}) 格式，第二个参数 jsonData 就是传到后端的数据。

```js
this.$http.get('get.php', { params: { a: 1, b: 2 } }).then(
  function (res) {
    document.write(res.body);
  },
  function (res) {
    console.log(res.status);
  }
);
```

## Post 请求

post 发送数据到后端，需要第三个参数 {emulateJSON:true}。

emulateJSON 的作用： 如果 Web 服务器无法处理编码为 application/json 的请求，可以启用 emulateJSON 选项。

```js
window.onload = function () {
  var vm = new Vue({
    el: '#box',
    data: {
      msg: 'Hello World!',
    },
    methods: {
      post: function () {
        //发送 post 请求
        this.$http
          .post('/try/ajax/demo_post.php', { name: '菜鸟教程', url: 'http://www.runoob.com' }, { emulateJSON: true })
          .then(
            function (res) {
              document.write(res.body);
            },
            function (res) {
              console.log(res.status);
            }
          );
      },
    },
  });
};
```

```php
# demo_post.php
<?php
$name = isset($_POST['name']) ? htmlspecialchars($_POST['name']) : '';
$city = isset($_POST['url']) ? htmlspecialchars($_POST['url']) : '';
echo '网站名: ' . $name;
echo "\n";
echo 'URL 地址: ' .$city;
?>
```

## 语法 & API

可以使用全局对象方式 Vue.http 或者在一个 Vue 实例的内部使用 this.$http 来发起 HTTP 请求。

```js
// 基于全局Vue对象使用http
Vue.http.get('/someUrl', [options]).then(successCallback, errorCallback);
Vue.http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);

// 在一个Vue实例内使用$http
this.$http.get('/someUrl', [options]).then(successCallback, errorCallback);
this.$http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);
```

vue-resource 提供了 7 种请求 API(REST 风格)：

```js
get(url, [options])
head(url, [options])
delete(url, [options])
jsonp(url, [options])
post(url, [body], [options])
put(url, [body], [options])
patch(url, [body], [options])
```

除了 jsonp 以外，另外 6 种的 API 名称是标准的 HTTP 方法。

options 参数说明:
| 参数 |	类型 |	描述 |
| :--: | :--: | :--: | 
| url |	string |	请求的目标URL |
| body |	Object, FormData, string |	作为请求体发送的数据 |
| headers |	Object |	作为请求头部发送的头部对象 |
| params |	Object |	作为URL参数的参数对象 |
| method |	string |	HTTP方法 (例如GET，POST，...) |
| timeout |	number |	请求超时（单位：毫秒） (0表示永不超时) |
| before |	function(request) |	在请求发送之前修改请求的回调函数 |
| progress |	function(event) |	用于处理上传进度的回调函数 ProgressEvent |
| credentials |	boolean |	是否需要出示用于跨站点请求的凭据 |
| emulateHTTP |	boolean |	是否需要通过设置X-HTTP-Method-Override头部并且以传统POST方式发送PUT，PATCH和DELETE请求。 |
| emulateJSON |	boolean |	设置请求体的类型为application/x-www-form-urlencoded |

通过如下属性和方法处理一个请求获取到的响应对象：
| 属性 |	类型 |	描述 |
| :--: | :--: | :--: | 
| url |	string |	响应的 URL 源 |
| body |	Object, Blob, string |	响应体数据 |
| headers |	Header |	请求头部对象 |
| ok |	boolean |	当 HTTP 响应码为 200 到 299 之间的数值时该值为 true |
| status |	number |	HTTP 响应码 |
| statusText |	string |	HTTP 响应状态 |


| 方法 |	类型 |	描述 |
| :--: | :--: | :--: | 
| text() |	约定值 |	以字符串方式返回响应体 |
| json() |	约定值 |	以格式化后的 json 对象方式返回响应体 |
| blob() |	约定值 |	以二进制 Blob 对象方式返回响应体 |

# Vue.js 响应接口

Vue 可以添加数据动态响应接口。

Vue 不允许在已经创建的实例上动态添加新的根级响应式属性。

Vue 不能检测到对象属性的添加或删除，最好的方式就是在初始化实例前声明根级响应式属性，哪怕只是一个空值。

如果需要在运行过程中实现属性的添加或删除，则可以使用全局 Vue，Vue.set 和 Vue.delete 方法。

## Vue.set

Vue.set 方法用于设置对象的属性，它可以解决 Vue 无法检测添加属性的限制，语法格式如下：

```js
Vue.set( target, key, value )
```

参数说明：
- target: 可以是对象或数组
- key : 可以是字符串或数字
- value: 可以是任何类型

## Vue.delete

Vue.delete 用于删除动态添加的属性 语法格式：

```js
Vue.delete( target, key )
```

参数说明：
- target: 可以是对象或数组
- key : 可以是字符串或数字