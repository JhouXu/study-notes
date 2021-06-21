# Vue.js 源码分析

## 分析

通过 MVVM 框架的实现基本功能模块

- 数据代理
- 模板解析
- 数据绑定

## 准备知识

1. [].slice.call(lis): 将伪数组转换为真数组

```js
[].slice.call(lis);

// 同理
Array.prototype.slice.call(lis);
```

2. node.nodeType: 得到节点类型
3. Object.defineProperty(obj, propName, {}): 给对象添加/修改属性(指定描述符)
   {} 属性描述符：

   - configurable：是否可以重新定义，删除。`默认为 false`。
   - enumerable：是否可以枚举。`默认为 false`。
   - 数据描述符
     - value：设置默认值。`默认为 undefined`。
     - writable：设置的 value 值是否可以赋值运算。`默认为 false`。
   - 存取描述符
     - get：返回当前属性值。
     - set：监听当前属性值变化。

```js
// Object.defineProperty(obj, propName, {}) demo：实现数据的监听
const obj = {
  firstName = 'A',
  lastName = 'B'
}
Object.defineProperty(obj, fullName, {
  get () {
    return firstName + '-' + lastName;
  },
  set (value) {
    let values = value.splice('-');
    this.firstName = values[0];
    this.lastName = values[1];
  }
})

console.log(obj.fullName) // A-B
fullName = "C-D" // firstName: C; lastName: D
```

4. Object.keys(obj): 得到对象自身可枚举的属性名的数组
5. DocumentFragment: 文档碎片(高效批量更新多个节点)

```html
<!-- DocumentFragment demo -->
<ul id="app">
  <li>test1</li>
  <li>test2</li>
  <li>test3</li>
</ul>
<script>
  const ul = document.getElementById("app");
  // 1. 创建 DocumentFragment 节点
  const fragment = document.createElement();
  // 2. 取出 ul 中所有子节点，并存储到 fragment 中
  let child;
  while ((child = ul.firstChild)) {
    // 一个节点只能有一个父亲
    fragment.appendChild(child); // 先将 child 在 ul 中移除，然后添加到 fragment 中
  }
  // 3. 更新 fragment 中所有的 li 文本
  Array.prototype.slice.call(fragment.childNodes).forEach((node) => {
    if (node.nodeType === 1) {
      // 判断是否为元素节点
      node.textContent = "更新 li 中的文本内容";
    }
  });
  // 4. 将 fragment 插入 ul 中
  ul.appendChild(fragment);
</script>
```

6. obj.hasOwnProperty(prop): 判断 prop 是否是 obj 自身的属性

## 一、数据代理

数据代理: 通过一个对象代理对另一个对象(在前一个对象内部)中属性的操作(读/写)。

vue 数据代理: 通过 vm 对象来代理 data 对象中所有属性的操作。

好处: 更方便的操作 data 中的数据。

基本实现流程：

1. 通过 Object.defineProperty()给 vm 添加与 data 对象的属性对应的属性描述符。
2. 所有添加的属性都包含 getter/setter。
3. getter/setter 内部去操作 data 中对应的属性数据。

## 二、模板解析

1. 将 el 的所有子节点取出, 添加到一个新建的文档 fragment 对象中。
2. 对 fragment 中的所有层次子节点递归进行编译解析处理。
   - 对大括号表达式文本节点进行解析
   - 对元素节点的指令属性进行解析
     - 事件指令解析
     - 一般指令解析
3. 将解析后的 fragment 添加到 el 中显示。

### 1. 大括号表达式解析

1. 根据正则对象得到匹配出的表达式字符串: `子匹配/RegExp.$1`。
2. 从 data 中取出表达式对应的属性值。
3. 将属性值设置为文本节点的 textContent。

```html
<div id="app">
  <p>{{ mag }}</p>
</div>
<script src="https://引入vue.js-cdn"></script>
<script>
  new Vue({
    el: '#app'
    data: {
      msg: '消息'
    }
  })
</script>
```

### 2. 事件指令解析

1. 从指令名中取出事件名
2. 根据指令的值(表达式)从 methods 中得到对应的事件处理函数对象。
3. 给当前元素节点绑定指定事件名和回调函数的 dom 事件监听。。
4. 指令解析完后, 移除此指令属性。

```html
<div id="app">
  <button v-on:click="alert"></button>
</div>
<script src="https://引入vue.js-cdn"></script>
<script>
  new Vue({
    el: '#app'
    methods: {
      alert () {
        alert('警告框生效')
      }
    }
  })
</script>
```

### 3. 一般指令解析

1. 得到指令名和指令值(表达式) text/html/class msg/myClass。
2. 从 data 中根据表达式得到对应的值。
3. 根据指令名确定需要操作元素节点的什么属性。
   - v-text---textContent 属性
   - v-html---innerHTML 属性
   - v-class--className 属性
4. 将得到的表达式的值设置到对应的属性上。
5. 移除元素的指令属性。

```html
<div id="app">
  <p v-text="msg"></p>
  <p v-html="msg"></p>
</div>
<script src="https://引入vue.js-cdn"></script>
<script>
  new Vue({
    el: '#app'
    data: {
      msg: '<a>测试</a>'
    }
  })
</script>
```

## 三、数据绑定

数据绑定：一旦更新了 data 中的某个属性数据, 所有界面上直接使用或间接使用了此属性的节点都会更新

### 数据劫持

数据劫持是 vue 中用来实现数据绑定的一种技术。

基本思想: 通过 defineProperty()来监视 data 中所有属性(任意层次)数据的变化, 一旦变化就去更新界面。

### 四个重要对象

1. Observer

- 用来对 data 所有属性数据进行劫持的构造函数。
- 给 data 中所有属性重新定义属性描述(get/set)。
- 为 data 中的每个属性创建对应的 dep 对象。

2. Dep(Depend)

- data 中的每个属性(所有层次)都对应一个 dep 对象。
- 创建的时机:
  - 在初始化 define data 中各个属性时创建对应的 dep 对象。
  - 在 data 中的某个属性值被设置为新的对象时。
- 对象的结构

```js
{
  id, // 每个 dep 都有一个唯一的 id
    subs; //包含 n 个对应 watcher 的数组(subscribes 的简写)
}
```

- subs 属性说明
  - 当 watcher 被创建时, 内部将当前 watcher 对象添加到对应的 dep 对象的 subs 中。
  - 当此 data 属性的值发生改变时, subs 中所有的 watcher 都会收到更新的通知,从而最终更新对应的界面。

3. Compiler

- 用来解析模板页面的对象的构造函数(一个实例) 。
- 利用 compile 对象解析模板页面。
- 每解析一个表达式(非事件指令)都会创建一个对应的 watcher 对象, 并建立 watcher 与 dep 的关系。
- complie 与 watcher 关系: 一对多的关系。

4. Watcher

- 模板中每个非事件指令或表达式都对应一个 watcher 对象
- 监视当前表达式数据的变化
- 创建的时机: 在初始化编译模板时
- 对象的组成

```js
{
  vm, //vm 对象
    exp, //对应指令的表达式
    cb, //当表达式所对应的数据发生改变的回调函数
    value, //表达式当前的值
    depIds; //表达式中各级属性所对应的 dep 对象的集合对象
  //属性名为 dep 的 id, 属性值为 dep
}
```

5. 总结: dep 与 watcher 的关系: 多对多

- data 中的一个属性对应一个 dep, 一个 dep 中可能包含多个 watcher(模板中有几个
  表达式使用到了同一个属性)
- 模板中一个非事件表达式对应一个 watcher, 一个 watcher 中可能包含多个 dep(表
  达式是多层: a.b)
- 数据绑定使用到 2 个核心技术
  - defineProperty() \* 消息订阅与发布

### 双向数据绑定

- 双向数据绑定是建立在单向数据绑定(model==>View)的基础之上的。
- 双向数据绑定的实现流程:
- 在解析 v-model 指令时, 给当前元素添加 input 监听。
- 当 input 的 value 发生改变时, 将最新的值赋值给当前表达式所对应的 data 属性。

### 程序关系流程图

![程序流程图](https://ftp.bmp.ovh/imgs/2021/06/bdd010704152d627.png)
