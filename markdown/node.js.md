# 什么是 node

简单的说 Node.js 就是运行在服务端的 JavaScript。
Node.js 是一个基于 Chrome JavaScript 运行时建立的一个平台。
Node.js 是一个事件驱动 I/O 服务端 JavaScript 环境，基于 Google 的 V8 引擎，V8 引擎执行 Javascript 的速度非常快，性能非常好。

```cmd
# 查看当前的 node 版本
$ node --version
```

# 创建第一个应用

## 创建 Node.js 应用

1. 引入 required 模块。

```js
var http = required('http');
```

2. 创建服务器

http.createServer() 方法创建服务器，并使用 listen 方法绑定 8888 端口。 函数通过 request, response 参数来接收和响应数据。

```js
var http = require('http');

http
  .createServer(function (request, response) {
    // 发送 HTTP 头部
    // HTTP 状态值: 200 : OK
    // 内容类型: text/plain
    response.writeHead(200, { 'Content-Type': 'text/plain' });

    // 发送响应数据 "Hello World"
    response.end('Hello World\n');
  })
  .listen(8888);

// 终端打印如下信息
console.log('Server running at http://127.0.0.1:8888/');
```

3. 运行

```cmd
# 运行 server.js 这个文件
$ node server.js
```

## 分析 Node.js 的 HTTP 服务器

- 第一行请求（require）Node.js 自带的 http 模块，并且把它赋值给 http 变量。

- 接下来我们调用 http 模块提供的函数： createServer 。这个函数会返回 一个对象，这个对象有一个叫做 listen 的方法，这个方法有一个数值参数， 指定这个 HTTP 服务器监听的端口号。

# npm 使用介绍

NPM 是随同 NodeJS 一起安装的包管理工具，能解决 NodeJS 代码部署上的很多问题，常见的使用场景有以下几种：

- 允许用户从 NPM 服务器下载别人编写的第三方包到本地使用。
- 允许用户从 NPM 服务器下载并安装别人编写的命令行程序到本地使用。
- 允许用户将自己编写的包或命令行程序上传到 NPM 服务器供别人使用。

```cmd
# 查看当前 npm 的版本
$ npm -v

# 升级 npm 到最新版本
$ npm install npm -g

# 使用淘宝镜像的命令
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## 使用 npm 命令安装模块

安装好之后，express 包就放在了工程目录下的 node_modules 目录中，因此在代码中只需要通过 require('express') 的方式就好，无需指定第三方包路径。

```cmd
# npm 安装 Node.js 模块语法格式
$ npm install <Module Name>
```

## 全局安装和本地安装

npm 的包安装分为本地安装（local）、全局安装（global）两种，从敲的命令行来看，差别只是有没有-g 而已。

```cmd
# 本地安装
$ npm install express

# 全局安装
$ npm install express -g
```

### 本地安装

1. 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
2. 可以通过 require() 来引入本地安装的包。

### 全局安装

1. 将安装包放在 /usr/local 下或者你 node 的安装目录。
2. 可以直接在命令行里使用。

如果你希望具备两者功能，则需要在两个地方安装它或使用 npm link。

### 查看安装版本信息

```cmd
# 查看所有全局安装的模块
$ npm list -g

# 查看某个模块的版本号
$ npm list <Module Name>
```

## 使用 package.json

package.json 位于模块的目录下，用于定义包的属性。

### package.json 属性说明。

- version - 表明了当前的版本。
- name - 设置了应用程序/软件包的名称。
- description - 是应用程序/软件包的简短描述。
- main - 设置了应用程序的入口点。require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 - index.js。
- private - 如果设置为 true，则可以防止应用程序/软件包被意外地发布到 npm。
- homepage - 包的官网 url 。
- author - 包的作者姓名。
- contributors - 包的其他贡献者姓名。
- repository - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
- keywords - 关键字。
- scripts - 定义了一组可以运行的 node 脚本。
- dependencies - 设置了作为依赖安装的 npm 软件包的列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
- devDependencies - 设置了作为开发依赖安装的 npm 软件包的列表。
- engines - 设置了此软件包/应用程序在哪个版本的 Node.js 上运行。
- browserslist - 用于告知要支持哪些浏览器（及其版本）。

## 卸载模块

```cmd
# 卸载 node.js 模块
$ npm uninstall <Module Name>

# 卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看
$ npm ls
```

## 更新模块

```cmd
# 更新 node.js 模块
$ npm update <Module Name>
```

## 搜索模块

```cmd
# 搜索 node.js 模块
$ npm search <Module Name>
```

## 创建模块

创建模块，package.json 文件是必不可少的。我们可以使用 NPM 生成 package.json 文件，生成的文件包含了基本的结果。

```cmd
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (node_modules) runoob                   # 模块名
version: (1.0.0)
description: Node.js 测试模块(www.runoob.com)  # 描述
entry point: (index.js)
test command: make test
git repository: https://github.com/runoob/runoob.git  # Github 地址
keywords:
author:
license: (ISC)
About to write to ……/node_modules/package.json:      # 生成地址

{
  "name": "runoob",
  "version": "1.0.0",
  "description": "Node.js 测试模块(www.runoob.com)",
  ……
}


Is this ok? (yes) yes       # 输入 yes 后会生成 package.json 文件。
```

接下来我们可以使用以下命令在 npm 资源库中注册用户（使用邮箱注册）：

```cmd
$ npm adduser
Username: mcmohd
Password:
Email: (this IS public) mcmohd@gmail.com
```

接下来我们就用以下命令来发布模块：

```cmd
$ npm publish
```

如果以上的步骤都操作正确，就可以跟其他模块一样使用 npm 来安装。

## 版本号

使用 NPM 下载和发布代码时都会接触到版本号。NPM 使用语义版本号来管理代码，这里简单介绍一下。

语义版本号分为 X.Y.Z 三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新。

- 如果只是修复 bug，需要更新 Z 位。
- 如果是新增了功能，但是向下兼容，需要更新 Y 位。
- 如果有大变动，向下不兼容，需要更新 X 位。

版本号有了这个保证后，在申明第三方包依赖时，除了可依赖于一个固定版本号外，还可依赖于某个范围的版本号。例如"argv": "0.0.x"表示依赖于 0.0.x 系列的最新版 argv。

NPM 支持的所有版本号范围指定方式可以查看[官方文档](https://www.npmjs.com/doc/files/package.json.html#dependencies)。

## NPM 常用命令

- NPM 提供了很多命令，例如 install 和 publish，使用 npm help 可查看所有命令。
- 使用 npm help <command>可查看某条命令的详细帮助，例如 npm help install。
- 在 package.json 所在目录下使用 npm install . -g 可先在本地安装当前命令行程序，可用于发布前的本地测试。
- 使用 npm update <package>可以把当前目录下 node_modules 子目录里边的对应模块更新至最新版本。
- 使用 npm update <package> -g 可以把全局安装的对应命令行程序更新至最新版。
- 使用 npm cache clear 可以清空 NPM 本地缓存，用于对付使用相同版本号发布新版本代码的人。
- 使用 npm unpublish <package>@<version>可以撤销发布自己发布过的某个版本代码。

## 使用淘宝 NPM 镜像

大家都知道国内直接使用 npm 的官方镜像是非常慢的，这里推荐使用淘宝 NPM 镜像。

淘宝 NPM 镜像是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10 分钟 一次以保证尽量与官方服务同步。

你可以使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:

```cmd
# 载入淘宝 NPM 镜像
$ npm install -g cnpm --registry=https://registry.npm.taobao.org

# 使用 cnpm 安装模块
$ cnpm install <Module Name>
```

# Node.js REPL(交互式解释器)

Node.js REPL(Read Eval Print Loop:交互式解释器) 表示一个电脑的环境，类似 Window 系统的终端或 Unix/Linux shell，我们可以在终端中输入命令，并接收系统的响应。

Node 自带了交互式解释器，可以执行以下任务：

- **读取** - 读取用户输入，解析输入的 Javascript 数据结构并存储在内存中。
- **执行** - 执行输入的数据结构。
- **打印** - 输出结果。
- **循环** - 循环操作以上步骤直到用户两次按下 ctrl-c 按钮退出。

```cmd
# 启动 Node 的终端
$ node
>
```

## 简单的表达式运算

```cmd
$ node
> 1 +4
5
```

## 使用变量

变量声明需要使用 var 关键字，如果没有使用 var 关键字变量会直接打印出来。

使用 var 关键字的变量可以使用 console.log() 来输出变量。

```cmd
$ node

> x = 10
10

> var y = 10
undefined

> console.log(y)
10
```

## 多行表达式

Node REPL 支持输入多行表达式。

```cmd
$ node
> for (let i = 0; i < 5; i++ ) {
... console.log(`x:` + i)
... }
x:0
x:1
x:2
x:3
x:4
undefined
>
```

... 三个点的符号是系统自动生成的，你回车换行后即可。Node 会自动检测是否为连续的表达式，括号是否完整关闭。

## 下划线(\_)变量

可以使用下划线(\_)获取上一个表达式的运算结果。

```cmd
$ node
> var a = 10
undefined
> var b = 100
undefined
> a+b
110
> console.log(_)
110
undefined
>
```

## REPL 命令

- ctrl + c - 退出当前终端。
- ctrl + c 按下两次 - 退出 Node REPL。
- ctrl + d - 退出 Node REPL.
- 向上/向下 键 - 查看输入的历史命令
- tab 键 - 列出当前命令
- .help - 列出使用命令
- .break - 退出多行表达式
- .clear - 退出多行表达式
- .save filename - 保存当前的 Node REPL 会话到指定文件
- .load filename - 载入当前 Node REPL 会话的文件内容。

## 停止 REPL

前面我们已经提到按下两次 ctrl + c 键就能退出 REPL。

```cmd
$ node
>
(^C again to quit)
>
```

# Node.js 回调函数

Node.js 异步编程的直接体现就是回调。

异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。

回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。

因此，阻塞是按顺序执行的，而非阻塞是不需要按顺序的，所以如果需要处理回调函数的参数，我们就需要写在回调函数内。

# Node.js 事件循环

Node.js 是单进程单线程应用程序，但是因为 V8 引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。

Node.js 几乎每一个 API 都是支持回调函数的。

Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。

Node.js 单线程类似进入一个 while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数。

## 事件驱动程序

Node.js 使用事件驱动模型，当 web server 接收到请求，就把它关闭然后进行处理，然后去服务下一个 web 请求。

当这个请求完成，它被放回处理队列，当到达队列开头，这个结果被返回给用户。

这个模型非常高效可扩展性非常强，因为 webserver 一直接受请求而不等待任何读写操作。（这也称之为非阻塞式 IO 或者事件驱动 IO）

在事件驱动模型中，会生成一个主循环来监听事件，当检测到事件时触发回调函数。

![event_loop.jpg](https://i.loli.net/2021/05/17/YGI52lkaQHecg3L.jpg)

Node.js 有多个内置的事件，我们可以通过引入 events 模块，并通过实例化 EventEmitter 类来绑定和监听事件：

```js
// 1-1 引入 events 模块
var events = require('events');
// 1-2 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();

// 2 绑定事件及事件的处理程序
eventEmitter.on('eventName', eventHandler);

// 3 触发事件
eventEmitter.emit('eventName');
```

## Node 应用程序是如何工作的？

在 Node 应用程序中，执行异步操作的函数将回调函数作为最后一个参数， 回调函数接收错误对象作为第一个参数。

例如:

```js
// input.txt
www.baidu.com;

// main.js
var fs = require('fs');

fs.readFile('input.txt', function (err, data) {
  if (err) {
    console.log(err.stack);
    return;
  }
  console.log(data.toString());
});
console.log('程序执行完毕');
```

以上程序中 fs.readFile() 是异步函数用于读取文件。 如果在读取文件过程中发生错误，错误 err 对象就会输出错误信息。

如果没发生错误，readFile 跳过 err 对象的输出，文件内容就通过回调函数输出。

# Node.js EventEmitter(事件触发器)

Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。

Node.js 里面的许多对象都会分发事件：一个 net.Server 对象会在每次有新连接时触发一个事件， 一个 fs.readStream 对象会在文件被打开的时候触发一个事件。 所有这些产生事件的对象都是 events.EventEmitter 的实例。

## EventEmitter 类(事件触发器)

events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装。

可以通过 require("events");来访问该模块。

```js
// 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();
```

EventEmitter 对象如果在实例化时发生错误，会触发 error 事件。当添加新的监听器时，newListener 事件会触发，当监听器被移除时，removeListener 事件被触发。

当事件触发时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。例如：

```js
//event.js 文件
var events = require('events');
var emitter = new events.EventEmitter();
emitter.on('someEvent', function (arg1, arg2) {
  console.log('listener1', arg1, arg2);
});
emitter.on('someEvent', function (arg1, arg2) {
  console.log('listener2', arg1, arg2);
});
emitter.emit('someEvent', 'arg1 参数', 'arg2 参数');
```

```cmd
# 运行结果
$ node event.js
listener1 arg1 参数 arg2 参数
listener2 arg1 参数 arg2 参数
```

emitter 为事件 someEvent 注册了两个事件监听器，然后触发了 someEvent 事件；运行结果中可以看到两个事件监听器回调函数被先后调用。 这就是 EventEmitter 最简单的用法。

EventEmitter 提供了多个属性，如 on 和 emit。on 函数用于绑定事件函数，emit 属性用于触发一个事件。接下来我们来具体看下 EventEmitter 的属性介绍。

### 方法

|                方法                |                                                           描述                                                           |
| :--------------------------------: | :----------------------------------------------------------------------------------------------------------------------: |
|    addListener(event, listener)    |                                       为指定事件添加一个监听器到监听器数组的尾部。                                       |
|        on(event, listener)         |                             为指定事件注册一个监听器，接受一个字符串 event 和一个回调函数。                              |
|       once(event, listener)        |                    为指定事件注册一个单次监听器，即 监听器最多只会触发一次，触发后立刻解除该监听器。                     |
|  removeListener(event, listener)   | 移除指定事件的某个监听器，监听器必须是该事件已经注册过的监听器。它接受两个参数，第一个是事件名称，第二个是回调函数名称。 |
|    removeAllListeners([event])     |                          移除所有事件的所有监听器， 如果指定事件，则移除指定事件的所有监听器。                           |
|         setMaxListeners(n)         |                        默认情况下， EventEmitters 如果你添加的监听器超过 10 个就会输出警告信息。                         |
|          setMaxListeners           |                                           函数用于改变监听器的默认限制的数量。                                           |
|          listeners(event)          |                                                返回指定事件的监听器数组。                                                |
| emit(event, [arg1], [arg2], [...]) |                     按监听器的顺序执行执行每个监听器，如果事件有注册监听返回 true，否则返回 false。                      |

### 类方法

|            类方法             |            描述            |
| :---------------------------: | :------------------------: |
| listenerCount(emitter, event) | 返回指定事件的监听器数量。 |

```js
events.EventEmitter.listenerCount(emitter, eventName); //已废弃，不推荐
events.emitter.listenerCount(eventName); //推荐
```

### 事件

|      事件      |                                                                          描述                                                                           |
| :------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------: |
|  newListener   |                                    event - 字符串，事件名称；listener - 处理事件函数；该事件在添加新监听器时被触发。                                    |
| removeListener | event - 字符串，事件名称；listener - 处理事件函数；从指定监听器数组中删除一个监听器。需要注意的是，此操作将会改变处于被删监听器之后的那些监听器的索引。 |

## error 事件

EventEmitter 定义了一个特殊的事件 error，它包含了错误的语义，我们在遇到 异常的时候通常会触发 error 事件。

当 error 被触发时，EventEmitter 规定如果没有响 应的监听器，Node.js 会把它当作异常，退出程序并输出错误信息。

我们一般要为会触发 error 事件的对象设置监听器，避免遇到错误后整个程序崩溃。

```js
var events = require('events');
var emitter = new events.EventEmitter();
emitter.emit('error');
```

## 继承 EventEmitter

大多数时候我们不会直接使用 EventEmitter，而是在对象中继承它。包括 fs、net、 http 在内的，只要是支持事件响应的核心模块都是 EventEmitter 的子类。

为什么要这样做呢？原因有两点：

首先，具有某个实体功能的对象实现事件**符合语义**， 事件的监听和发生应该是一个对象的方法。

其次 JavaScript 的对象机制是**基于原型**的，支持部分多重继承，继承 EventEmitter 不会打乱对象原有的继承关系。

# Node.js Buffer(缓冲区)

JavaScript 语言自身只有字符串数据类型，没有二进制数据类型。

但在处理像 TCP 流或文件流时，必须使用到二进制数据。因此在 Node.js 中，定义了一个 Buffer 类，该类用来创建一个专门存放二进制数据的缓存区。

在 Node.js 中，Buffer 类是随 Node 内核一起发布的核心库。Buffer 库为 Node.js 带来了一种存储原始数据的方法，可以让 Node.js 处理二进制数据，每当需要在 Node.js 中处理 I/O 操作中移动的数据时，就有可能使用 Buffer 库。原始数据存储在 Buffer 类的实例中。一个 Buffer 类似于一个整数数组，但它对应于 V8 堆内存之外的一块原始内存。

> 在 v6.0 之前创建 Buffer 对象直接使用 new Buffer()构造函数来创建对象实例，但是 Buffer 对内存的权限操作相比很大，可以直接捕获一些敏感信息，所以在 v6.0 以后，官方文档里面建议使用 Buffer.from() 接口去创建 Buffer 对象。

## Buffer 与字符编码

Buffer 实例一般用于表示编码字符的序列，比如 UTF-8 、 UCS2 、 Base64 、或十六进制编码的数据。 通过使用显式的字符编码，就可以在 Buffer 实例与普通的 JavaScript 字符串之间进行相互转换。

```js
const buf = Buffer.from('runoob', 'ascii');

// 输出 72756e6f6f62
console.log(buf.toString('hex'));

// 输出 cnVub29i
console.log(buf.toString('base64'));
```

Node.js 目前支持的字符编码包括：

- **ascii** - 仅支持 7 位 ASCII 数据。如果设置去掉高位的话，这种编码是非常快的。
- **utf8** - 多字节编码的 Unicode 字符。许多网页和其他文档格式都使用 UTF-8 。
- **utf16le** - 2 或 4 个字节，小字节序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。
- **ucs2** - utf16le 的别名。
- **base64** - Base64 编码。
- **latin1** - 一种把 Buffer 编码成一字节编码的字符串的方式。
- **binary** - latin1 的别名。
- **hex** - 将每个字节编码为两个十六进制字符。

## 创建 Buffer 类

|                        方法                        |                                                 描述                                                  |
| :------------------------------------------------: | :---------------------------------------------------------------------------------------------------: |
|      Buffer.alloc(size[, fill[, encoding]])：      |                    返回一个指定大小的 Buffer 实例，如果没有设置 fill，则默认填满 0                    |
|             Buffer.allocUnsafe(size)：             |             返回一个指定大小的 Buffer 实例，但是它不会被初始化，所以它可能包含敏感的数据              |
|            Buffer.allocUnsafeSlow(size)            |                                                  无                                                   |
|                Buffer.from(array)：                | 返回一个被 array 的值初始化的新的 Buffer 实例（传入的 array 的元素只能是数字，不然就会自动被 0 覆盖） |
| Buffer.from(arrayBuffer[, byteOffset[, length]])： |                      返回一个新建的与给定的 ArrayBuffer 共享同一内存的 Buffer。                       |
|               Buffer.from(buffer)：                |                       复制传入的 Buffer 实例的数据，并返回一个新的 Buffer 实例                        |
|         Buffer.from(string[, encoding])：          |                            返回一个被 string 的值初始化的新的 Buffer 实例                             |

```js
// 创建一个长度为 10、且用 0 填充的 Buffer。
const buf1 = Buffer.alloc(10);

// 创建一个长度为 10、且用 0x1 填充的 Buffer。
const buf2 = Buffer.alloc(10, 1);

// 创建一个长度为 10、且未初始化的 Buffer。
// 这个方法比调用 Buffer.alloc() 更快，
// 但返回的 Buffer 实例可能包含旧数据，
// 因此需要使用 fill() 或 write() 重写。
const buf3 = Buffer.allocUnsafe(10);

// 创建一个包含 [0x1, 0x2, 0x3] 的 Buffer。
const buf4 = Buffer.from([1, 2, 3]);

// 创建一个包含 UTF-8 字节 [0x74, 0xc3, 0xa9, 0x73, 0x74] 的 Buffer。
const buf5 = Buffer.from('tést');

// 创建一个包含 Latin-1 字节 [0x74, 0xe9, 0x73, 0x74] 的 Buffer。
const buf6 = Buffer.from('tést', 'latin1');
```

## 写入缓冲区

### 语法

```js
buf.write(string[, offset[, length]][, encoding])
```

### 参数

- **string** - 写入缓冲区的字符串。
- **offset** - 缓冲区开始写入的索引值，默认为 0 。
- **length** - 写入的字节数，默认为 buffer.length
- **encoding** - 使用的编码。默认为 'utf8' 。

根据 encoding 的字符编码写入 string 到 buf 中的 offset 位置。 length 参数是写入的字节数。 如果 buf 没有足够的空间保存整个字符串，则只会写入 string 的一部分。 只部分解码的字符不会被写入。

### 返回值

返回实际写入的大小。如果 buffer 空间不足， 则只会写入部分字符串。

### 实例

```js
buf = Buffer.alloc(256);
len = buf.write('www.baidu.com');

console.log('写入字节数 : ' + len);
// 输出：写入字节数 : 13
```

## 冲缓存区读取数据

### 语法

```js
buf.toString([encoding[, start[, end]]])
```

### 参数

- **encoding** - 使用的编码。默认为 'utf8' 。
- **start** - 指定开始读取的索引位置，默认为 0。
- **end** - 结束位置，默认为缓冲区的末尾。

### 返回值

解码缓冲区数据并使用指定的编码返回字符串。

### 实例

```js
buf = Buffer.alloc(26);
for (var i = 0; i < 26; i++) {
  buf[i] = i + 97;
}

console.log(buf.toString('ascii')); // 输出: abcdefghijklmnopqrstuvwxyz
console.log(buf.toString('ascii', 0, 5)); //使用 'ascii' 编码, 并输出: abcde
console.log(buf.toString('utf8', 0, 5)); // 使用 'utf8' 编码, 并输出: abcde
console.log(buf.toString(undefined, 0, 5)); // 使用默认的 'utf8' 编码, 并输出: abcde

// 分别输出：
// abcdefghijklmnopqrstuvwxyz
// abcde
// abcde
// abcde
```

## 将 Buffer 转换为 JSON 对象

### 语法

```js
buf.toJSON();
```

### 返回值

返回 JSON 对象。

### 实例

```js
const buf = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5]);
const json = JSON.stringify(buf);

// 输出: {"type":"Buffer","data":[1,2,3,4,5]}
console.log(json);
```

## 缓冲区合并

### 语法

```js
Buffer.concat(list[, totalLength])
```

### 参数

- **list** - 用于合并的 Buffer 对象数组列表。
- **totalLength** - 指定合并后 Buffer 对象的总长度。

### 返回值

返回一个多个成员合并的新 Buffer 对象。

### 实例

```js
var buffer1 = Buffer.from('百度一下');
var buffer2 = Buffer.from('www.baidu.com');
var result = Buffer.concat([buffer1, buffer2]);
console.log('result 内容: ' + result.toString());
// 输出：result 内容: 百度一下www.baidu.com
```

## 缓冲区比较

### 语法

```js
buf.compare(otherBuffer);
```

### 参数

- **otherBuffer** - 与 buf 对象比较的另外一个 Buffer 对象。

### 返回值

返回一个数字，表示 buf 在 otherBuffer 之前，之后或相同。

### 实例

```js
var buffer1 = Buffer.from('ABC');
var buffer2 = Buffer.from('ABCD');
var result = buffer1.compare(buffer2);

if (result < 0) {
  console.log(buffer1 + ' 在 ' + buffer2 + '之前');
} else if (result == 0) {
  console.log(buffer1 + ' 与 ' + buffer2 + '相同');
} else {
  console.log(buffer1 + ' 在 ' + buffer2 + '之后');
}
// 输出：ABC在ABCD之前
```

## 拷贝缓存区

### 语法

```js
buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]])
```

### 参数

- **targetBuffer** - 要拷贝的 Buffer 对象。
- **targetStart** - 数字, 可选, 默认: 0
- **sourceStart** - 数字, 可选, 默认: 0
- **sourceEnd** - 数字, 可选, 默认: buffer.length

### 返回值

无返回值。

### 实例

```js
var buf1 = Buffer.from('abcdefghijkl');
var buf2 = Buffer.from('RUNOOB');

//将 buf2 插入到 buf1 指定位置上
buf2.copy(buf1, 2);

console.log(buf1.toString());
// 输出：abRUNOOBijkl
```

## 缓冲区裁剪

### 语法

```js
buf.slice([start[, end]])
```

### 参数

- **start** - 数字, 可选, 默认: 0
- **end** - 数字, 可选, 默认: buffer.length

### 返回值

返回一个新的缓冲区，它和旧缓冲区指向同一块内存，但是从索引 start 到 end 的位置剪切。

### 实例

```js
var buffer1 = Buffer.from('runoob');
// 剪切缓冲区
var buffer2 = buffer1.slice(0, 2);
console.log('buffer2 content: ' + buffer2.toString());
// 输出：buffer2 content: ru
```

## 缓冲区长度

### 语法

```js
buf.length;
```

### 返回值

返回 Buffer 对象所占据的内存长度。

### 实例

```js
var buffer = Buffer.from('www.runoob.com');
//  缓冲区长度
console.log('buffer length: ' + buffer.length);
// 输出：buffer length: 14
```

## 方法参考手册

|                               方法                                |                                                                                                                                                                                 描述                                                                                                                                                                                 |
| :---------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | 
|                         new Buffer(size)                          |                                                                                           分配一个新的 size 大小单位为 8 位字节的 buffer。 注意, size 必须小于 kMaxLength，否则，将会抛出异常 RangeError。`废弃的: 使用 Buffer.alloc() 代替（或 Buffer.allocUnsafe()）`。                                                                                            |
|                        new Buffer(buffer)                         |                                                                                                                                           拷贝参数 buffer 的数据到 Buffer 实例。`废弃的: 使用 Buffer.from(buffer) 代替`。                                                                                                                                            |
|                    new Buffer(str[, encoding])                    |                                                                                                              分配一个新的 buffer ，其中包含着传入的 str 字符串。 encoding 编码方式默认为 'utf8'。 `废弃的: 使用 Buffer.from(string[, encoding]) 代替`。                                                                                                              |
|                            buf.length                             |                                                                                                          返回这个 buffer 的 bytes 数。注意这未必是 buffer 里面内容的大小。length 是 buffer 对象所分配的内存数，它不会随着这个 buffer 对象内容的改变而改变。                                                                                                          |
|         buf.write(string[, offset[, length]][, encoding])         |                                                                                                              根据参数 offset 偏移量和指定的 encoding 编码方式，将参数 string 数据写入 buffer。 offset 偏移量默认值是 0, encoding 编码方式默认是 utf8。                                                                                                               | length 长度是将要写入的字符串的 bytes 大小。 返回 number 类型，表示写入了多少 8 位字节流。如果 buffer 没有足够的空间来放整个 string，它将只会只写入部分字符串。 length 默认是 buffer.length - offset。 这个方法不会出现写入部分字符。 |
|      buf.writeUIntLE(value, offset, byteLength[, noAssert])       |                                                                                                                                   将 value 写入到 buffer 里， 它由 offset 和 byteLength 决定，最高支持 48 位无符号整数，小端对齐。                                                                                                                                   |
|      buf.writeUIntBE(value, offset, byteLength[, noAssert])       |                                                                                              将 value 写入到 buffer 里， 它由 offset 和 byteLength 决定，最高支持 48 位无符号整数，大端对齐。noAssert 值为 true 时，不再验证 value 和 offset 的有效性。 默认是 false。                                                                                               |
|       buf.writeIntLE(value, offset, byteLength[, noAssert])       |                                                                                              将 value 写入到 buffer 里， 它由 offset 和 byteLength 决定，最高支持 48 位有符号整数，小端对齐。noAssert 值为 true 时，不再验证 value 和 offset 的有效性。 默认是 false。                                                                                               |
|       buf.writeIntBE(value, offset, byteLength[, noAssert])       |                                                                                              将 value 写入到 buffer 里， 它由 offset 和 byteLength 决定，最高支持 48 位有符号整数，大端对齐。noAssert 值为 true 时，不再验证 value 和 offset 的有效性。 默认是 false。                                                                                               |
|          buf.readUIntLE(offset, byteLength[, noAssert])           |                                                                                                                       支持读取 48 位以下的无符号数字，小端对齐。noAssert 值为 true 时， offset 不再验证是否超过 buffer 的长度，默认为 false。                                                                                                                        |
|          buf.readUIntBE(offset, byteLength[, noAssert])           |                                                                                                                       支持读取 48 位以下的无符号数字，大端对齐。noAssert 值为 true 时， offset 不再验证是否超过 buffer 的长度，默认为 false。                                                                                                                        |
|           buf.readIntLE(offset, byteLength[, noAssert])           |                                                                                                                       支持读取 48 位以下的有符号数字，小端对齐。noAssert 值为 true 时， offset 不再验证是否超过 buffer 的长度，默认为 false。                                                                                                                        |
|           buf.readIntBE(offset, byteLength[, noAssert])           |                                                                                                                       支持读取 48 位以下的有符号数字，大端对齐。noAssert 值为 true 时， offset 不再验证是否超过 buffer 的长度，默认为 false。                                                                                                                        |
|             buf.toString([encoding[, start[, end]]])              |                                                                                                           根据 encoding 参数（默认是 'utf8'）返回一个解码过的 string 类型。还会根据传入的参数 start (默认是 0) 和 end (默认是 buffer.length)作为取值范围。                                                                                                           |
|                           buf.toJSON()                            |                                                                                                                                                                   将 Buffer 实例转换为 JSON 对象。                                                                                                                                                                   |
|                            buf[index]                             |                                                                                                                             获取或设置指定的字节。返回值代表一个字节，所以返回值的合法范围是十六进制 0x00 到 0xFF 或者十进制 0 至 255。                                                                                                                              |
|                      buf.equals(otherBuffer)                      |                                                                                                                                                      比较两个缓冲区是否相等，如果是返回 true，否则返回 false。                                                                                                                                                       |
|                     buf.compare(otherBuffer)                      |                                                                                                                                            比较两个 Buffer 对象，返回一个数字，表示 buf 在 otherBuffer 之前，之后或相同。                                                                                                                                            |
| buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]]) |                                                                                                        buffer 拷贝，源和目标可以相同。 targetStart 目标开始偏移和 sourceStart 源开始偏移默认都是 0。 sourceEnd 源结束位置偏移默认是源的长度 buffer.length 。                                                                                                         |
|                     buf.slice([start[, end]])                     |                                                                                                                    剪切 Buffer 对象，根据 start(默认是 0 ) 和 end (默认是 buffer.length ) 偏移和裁剪了索引。 负的索引是从 buffer 尾部开始计算的。                                                                                                                    |
|                 buf.readUInt8(offset[, noAssert])                 |                                                                                                      根据指定的偏移量，读取一个无符号 8 位整数。若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 如果这样 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                                      |
|               buf.readUInt16LE(offset[, noAssert])                |                                                                                       根据指定的偏移量，使用特殊的 endian 字节序格式读取一个无符号 16 位整数。若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                        |
|               buf.readUInt16BE(offset[, noAssert])                |                                                                                  根据指定的偏移量，使用特殊的 endian 字节序格式读取一个无符号 16 位整数，大端对齐。若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                   |
|               buf.readUInt32LE(offset[, noAssert])                |                                                                                  根据指定的偏移量，使用指定的 endian 字节序格式读取一个无符号 32 位整数，小端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                  |
|               buf.readUInt32BE(offset[, noAssert])                |                                                                                  根据指定的偏移量，使用指定的 endian 字节序格式读取一个无符号 32 位整数，大端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                  |
|                 buf.readInt8(offset[, noAssert])                  |                                                                                                     根据指定的偏移量，读取一个有符号 8 位整数。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                                      |
|                buf.readInt16LE(offset[, noAssert])                |                                                                                    根据指定的偏移量，使用特殊的 endian 格式读取一个 有符号 16 位整数，小端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                     |
|                buf.readInt16BE(offset[, noAssert])                |                                                                                    根据指定的偏移量，使用特殊的 endian 格式读取一个 有符号 16 位整数，大端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                     |
|                buf.readInt32LE(offset[, noAssert])                |                                                                                  根据指定的偏移量，使用指定的 endian 字节序格式读取一个有符号 32 位整数，小端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                  |
|                buf.readInt32BE(offset[, noAssert])                |                                                                                  根据指定的偏移量，使用指定的 endian 字节序格式读取一个有符号 32 位整数，大端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                  |
|                buf.readFloatLE(offset[, noAssert])                |                                                                                   根据指定的偏移量，使用指定的 endian 字节序格式读取一个 32 位双浮点数，小端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                   |
|                buf.readFloatBE(offset[, noAssert])                |                                                                                   根据指定的偏移量，使用指定的 endian 字节序格式读取一个 32 位双浮点数，大端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                   |
|               buf.readDoubleLE(offset[, noAssert])                |                                                                                   根据指定的偏移量，使用指定的 endian 字节序格式读取一个 64 位双精度数，小端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                   |
|               buf.readDoubleBE(offset[, noAssert])                |                                                                                   根据指定的偏移量，使用指定的 endian 字节序格式读取一个 64 位双精度数，大端对齐。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 offset 可能会超出 buffer 的末尾。默认是 false。                                                                                   |
|             buf.writeUInt8(value, offset[, noAssert])             |                                   根据传入的 offset 偏移量将 value 写入 buffer。注意：value 必须是一个合法的无符号 8 位整数。 若参数 noAssert 为 true 将不会验证 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则不要使用。默认是 false。                                   |
|           buf.writeUInt16LE(value, offset[, noAssert])            |             根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个合法的无符号 16 位整数，小端对齐。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。             |
|           buf.writeUInt16BE(value, offset[, noAssert])            |             根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个合法的无符号 16 位整数，大端对齐。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。             |
|           buf.writeUInt32LE(value, offset[, noAssert])            | 根据传入的 offset 偏移量和指定的 endian 格式(LITTLE-ENDIAN:小字节序)将 value 写入 buffer。注意：value 必须是一个合法的无符号 32 位整数，小端对齐。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。 |
|           buf.writeUInt32BE(value, offset[, noAssert])            |       根据传入的 offset 偏移量和指定的 endian 格式(Big-Endian:大字节序)将 value 写入 buffer。注意：value 必须是一个合法的有符号 32 位整数。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。        |
|             buf.writeInt8(value, offset[, noAssert])              |                                                                                                                                                                                  无                                                                                                                                                                                  |
|            buf.writeInt16LE(value, offset[, noAssert])            |                 根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个合法的 signed 16 位整数。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false 。                 |
|            buf.writeInt16BE(value, offset[, noAssert])            |                 根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个合法的 signed 16 位整数。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false 。                 |
|            buf.writeInt32LE(value, offset[, noAssert])            |                 根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个合法的 signed 32 位整数。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。                  |
|            buf.writeInt32BE(value, offset[, noAssert])            |                 根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个合法的 signed 32 位整数。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。                  |
|            buf.writeFloatLE(value, offset[, noAssert])            |        根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer 。注意：当 value 不是一个 32 位浮点数类型的值时，结果将是不确定的。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。        |
|            buf.writeFloatBE(value, offset[, noAssert])            |        根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer 。注意：当 value 不是一个 32 位浮点数类型的值时，结果将是不确定的。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。        |
|           buf.writeDoubleLE(value, offset[, noAssert])            |               根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个有效的 64 位 double 类型的值。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。               |
|           buf.writeDoubleBE(value, offset[, noAssert])            |               根据传入的 offset 偏移量和指定的 endian 格式将 value 写入 buffer。注意：value 必须是一个有效的 64 位 double 类型的值。 若参数 noAssert 为 true 将不会验证 value 和 offset 偏移量参数。 这意味着 value 可能过大，或者 offset 可能会超出 buffer 的末尾从而造成 value 被丢弃。 除非你对这个参数非常有把握，否则尽量不要使用。默认是 false。               |
|                 buf.fill(value[, offset][, end])                  |                                                                                                                      使用指定的 value 来填充这个 buffer。如果没有指定 offset (默认是 0) 并且 end (默认是 buffer.length) ，将会填充整个 buffer。                                                                                                                      |

# Node.js Stream(流)

Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。例如，对 http 服务器发起请求的 request 对象就是一个 Stream，还有 stdout（标准输出）。

在 Node.js 中 Stream 的四种类型：

- **Readable** - 可读操作。
- **Writable** - 可写操作。
- **Duplex** - 可读可写操作.
- **Transform** - 操作被写入数据，然后读出结果。

所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：

- **data** - 当有数据可读时触发。
- **end** - 没有更多的数据可读时触发。
- **error** - 在接收和写入过程中发生错误时触发。
- **finish** - 所有数据已被写入到底层系统时触发。

## 从流中读取数据

```js
// input.txt
百度官网地址：www.baidu.com

// main.js
var fs = require("fs");
var data = '';
// 创建可读流
var readerStream = fs.createReadStream('input.txt');
// 设置编码为 utf8。
readerStream.setEncoding('UTF8');
// 处理流事件 --> data, end, and error
readerStream.on('data', function(chunk) {
   data += chunk;
});
readerStream.on('end',function(){
   console.log(data);
});
readerStream.on('error', function(err){
   console.log(err.stack);
});
console.log("程序执行完毕");

// 输出：
// 程序执行完毕
// 百度官网地址：www.baidu.com
```

## 写入流

```js
var fs = require('fs');
var data = '百度官网地址：www.baidu.com';
// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');
// 使用 utf8 编码写入数据
writerStream.write(data, 'UTF8');
// 标记文件末尾
writerStream.end();
// 处理流事件 --> finish、error
writerStream.on('finish', function () {
  console.log('写入完成。');
});
writerStream.on('error', function (err) {
  console.log(err.stack);
});
console.log('程序执行完毕');
// 输出：
// 会在 input.txt 文件中写入 百度官网地址：www.baidu.com 字符串
```

## 管道流

管道提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中。实现文件中的数据拷贝。

```js
// input.txt
管道流操作实例，百度官网地址：www.baidu.com

// main.js
var fs = require('fs');

// 创建一个可读流
var readerStream = fs.createReadStream('../data/input.txt');
// 创建一个可写流
var writeStream = fs.createWriteStream('../data/output.text');

// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream);

console.log("程序写入成功");
// 输出：
// 在 output.txt 文件中显示 管道流操作实例，百度官网地址：www.baidu.com 内容
```

## 链式流

链式是通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作。可以用来实现文件的压缩以及解压功能。

```js
// 文件压缩
var fs = require('fs');
var zlib = require('zlib');

// 压缩 input.txt 文件为 input.txt.zip
fs.createReadStream('../data/input.txt').pipe(zlib.createGzip()).pipe(fs.createWriteStream('../data/input.txt.zip'));
console.log('文件压缩完成。');

// 文件解压
// 解压 input.txt.zip 文件为 input.txt
fs.createReadStream('../data/input.txt.zip').pipe(zlib.createGunzip()).pipe(fs.createWriteStream('../data/input.txt'));
console.log('文件解压完成。');
```

# Node.js 模块系统

为了让 Node.js 的文件可以相互调用，Node.js 提供了一个简单的模块系统。

模块是 Node.js 应用程序的基本组成部分，文件和模块是一一对应的。换言之，一个 Node.js 文件就是一个模块，这个文件可能是 JavaScript 代码、JSON 或者编译过的 C/C++ 扩展。

## 引入模块

Node.js 提供了 exports 和 require 两个对象，其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。

```js
// main.js
var hello = require('./hello');
hello.world();
```

### 返回函数

```js
// hello.js
exports.world = function () {
  console.log('Hello World');
};
```

hello.js 通过 exports 对象把 world 作为模块的访问接口，在 main.js 中通过 require('./hello') 加载这个模块，然后就可以直接访问 hello.js 中 exports 对象的`成员函数`了。

### 返回对象

```js
module.exports = function () {
  // ...
};

// 例如：
// -hello.js
// function Hello() {
//   var name;
//   this.setName = function(thyName) {
//     name = thyName;
//   };
//   this.sayHello = function() {
//     console.log('Hello ' + name);
//   };
// };
// module.exports = Hello;
// 这样就可以直接获得这个对象了：

// -main.js
// var Hello = require('./hello');
// hello = new Hello();
// hello.setName('BYVoid');
// hello.sayHello();
```

模块接口的唯一变化是使用 module.exports = Hello 代替了 exports.world = function(){}。 在外部引用该模块时，其接口对象就是要输出的 Hello 对象本身，而不是原先的 exports。

## 服务端的模块放在哪里

Node.js 中自带了一个叫做 http 的模块，我们在我们的代码中请求它并把返回值赋给一个本地变量。这把我们的本地变量变成了一个拥有所有 http 模块所提供的公共方法的对象。

由于 Node.js 中存在 4 类模块（原生模块和 3 种文件模块）。

### require 方法内部加载

![nodejs-require.jpg](https://i.loli.net/2021/05/18/M4o1Rz2YpgB5mEK.jpg)

### 从文件模块缓存中加载

尽管原生模块与文件模块的优先级不同，但是都会优先从文件模块的缓存中加载已经存在的模块。

### 从原生模块加载

原生模块的优先级仅次于文件模块缓存的优先级。require 方法在解析文件名之后，优先检查模块是否在原生模块列表中。以 http 模块为例，尽管在目录下存在一个 http/http.js/http.node/http.json 文件，require("http") 都不会从这些文件中加载，而是从原生模块中加载。

原生模块也有一个缓存区，同样也是优先从缓存区加载。如果缓存区没有被加载过，则调用原生模块的加载方式进行加载和执行。

### 从文件加载

当文件模块缓存中不存在，而且不是原生模块的时候，Node.js 会解析 require 方法传入的参数，并从文件系统中加载实际的文件。

require 方法的参数传递方式：

- http、fs、path 等，原生模块。
- ./mod 或../mod，相对路径的文件模块。
- /pathtomodule/mod，绝对路径的文件模块。
- mod，非原生模块的文件模块。

> **exports 和 module.exports 的使用**
> 如果要对外暴露属性或方法，就用 exports 就行，要暴露对象(类似 class，包含了很多属性和方法)，就用 module.exports。

# Node.js 函数

## 普通函数创建以及调用

```js
// 子函数
function say(word) {
  console.log(word);
}

// 函数调用工厂
function execute(someFunction, value) {
  someFunction(value);
}

execute(say, 'Hello');
```

### 匿名函数

可以把一个函数作为变量传递。但是不一定要绕这个"先定义，再传递"的圈子，我们可以直接在另一个函数的括号中定义和传递这个函数。

```js
function execute(someFunction, value) {
  someFunction(value);
}

execute(function (word) {
  console.log(word);
}, 'Hello');
```

### 函数传递是如何让 HTTP 服务器工作的

```js
// 普通函数
var http = require('http');
http
  .createServer(function (request, response) {
    response.writeHead(200, { 'Content-Type': 'text/plain' });
    response.write('Hello World');
    response.end();
  })
  .listen(8888);

// 匿名函数
var http = require('http');
function onRequest(request, response) {
  response.writeHead(200, { 'Content-Type': 'text/plain' });
  response.write('Hello World');
  response.end();
}
http.createServer(onRequest).listen(8888);
```

# Node.js 路由

需要的所有数据都会包含在 request 对象中，该对象作为 onRequest() 回调函数的第一个参数传递。但是为了解析这些数据，需要额外的 Node.JS 模块，它们分别是 url 和 querystring 模块。

也可以用 querystring 模块来解析 POST 请求体中的参数。

![Snipaste_2021-05-18_11-49-43.png](https://i.loli.net/2021/05/18/edjO2yBCfD8iVz5.png)

## 路由实现

```js
// index.js
var server = require('./server');
var router = require('./router');
server.start(router.route);

// server.js
var http = require('http');
var url = require('url');
function start(route) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log('Request for ' + pathname + ' received.');
    route(pathname);
    response.writeHead(200, { 'Content-Type': 'text/plain' });
    response.write('Hello World!');
    response.end();
  }
  http.createServer(onRequest).listen(8888);
  console.log('Server has started');
}
exports.start = start;

// router.js
function route(pathname) {
  console.log('About to route a request for ' + pathname);
}
exports.route = route;
```

# Node.js 全局对象

JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。

在浏览器 JavaScript 中，通常 window 是全局对象， 而 Node.js 中的全局对象是 `global`，所有全局变量（除了 global 本身以外）都是 global 对象的属性。

## 全局对象与全局变量

global 最根本的作用是作为全局变量的宿主。

按照 ECMAScript 的定义，满足以下条件的变量是全局变量：

- 在最外层定义的变量；
- 全局对象的属性；
- 隐式定义的变量（未定义直接赋值的变量）。

## \_\_filename

\_\_filename 表示当前正在执行的脚本的文件名。它将输出文件所在位置的绝对路径，且和命令行参数所指定的文件名不一定相同。 如果在模块中，返回的值是模块文件的路径。

## \_\_dirname

\_\_dirname 表示当前执行脚本所在的目录。

## setTimeout(cb, ms)

setTimeout(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。：setTimeout() 只执行一次指定函数。返回一个代表定时器的句柄值。

## clearTimeout(t)

clearTimeout( t ) 全局函数用于停止一个之前通过 setTimeout() 创建的定时器。 参数 t 是通过 setTimeout() 函数创建的定时器。

## setInterval(cb, ms)

setInterval(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。返回一个代表定时器的句柄值。可以使用 clearInterval(t) 函数来清除定时器。
setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。

## console

console 用于提供控制台标准输出，它是由 Internet Explorer 的 JScript 引擎提供的调试工具，后来逐渐成为浏览器的实施标准。

Node.js 沿用了这个标准，提供与习惯行为一致的 console 对象，用于向标准输出流（stdout）或标准错误流（stderr）输出字符。

### console 方法

|                  方法                   |                                                                                 描述                                                                                  |
| :-------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|       console.log([data][, ...])        | 向标准输出流打印字符并以换行符结束。该方法接收若干 个参数，如果只有一个参数，则输出这个参数的字符串形式。如果有多个参数，则 以类似于 C 语言 printf() 命令的格式输出。 |
|       console.info([data][, ...])       |                    该命令的作用是返回信息性消息，这个命令与 console.log 差别并不大，除了在 chrome 中只会输出文字外，其余的会显示一个蓝色的惊叹号。                    |
|      console.error([data][, ...])       |                                                        输出错误消息的。控制台在出现错误时会显示是红色的叉子。                                                         |
|       console.warn([data][, ...])       |                                                               输出警告消息。控制台出现有黄色的惊叹号。                                                                |
|       console.dir(obj[, options])       |                                                   用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示。                                                   |
|           console.time(label)           |                                                                       输出时间，表示计时开始。                                                                        |
|         console.timeEnd(label)          |                                                                       结束时间，表示计时结束。                                                                        |
|      console.trace(message[, ...])      |                             当前执行的代码在堆栈中的调用路径，这个测试函数运行很有帮助，只要给想测试的函数里面加入 console.trace 就行了。                             |
| console.assert(value[, message][, ...]) |      用于判断某个表达式或变量是否为真，接收两个参数，第一个参数是表达式，第二个参数是字符串。只有当第一个参数为 false，才会输出第二个参数，否则不会有任何结果。       |

### 实例

```js
// 向标准错误流输出当前的调用栈。
console.trace();

// 输出：
// Trace:
// at Object.<anonymous> (/home/byvoid/consoletrace.js:1:71)
// at Module._compile (module.js:441:26)
// at Object..js (module.js:459:10)
// at Module.load (module.js:348:31)
// at Function._load (module.js:308:12)
// at Array.0 (module.js:479:10)
// at EventEmitter._tickCallback (node.js:192:40)
```

## process

process 是一个全局变量，即 global 对象的属性。

它用于描述当前 Node.js 进程状态的对象，提供了一个与操作系统的简单接口。常用于编写本地命令行程序时。

### process 事件

|       事件        |                                                                             描述                                                                             |
| :---------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------: |
|       exit        |                                                                    当进程准备退出时触发。                                                                    |
|    beforeExit     | 当 node 清空事件循环，并且没有其他安排时触发这个事件。通常来说，当没有进程安排时 node 退出，但是 'beforeExit' 的监听器可以异步调用，这样 node 就会继续执行。 |
| uncaughtException |                      当一个异常冒泡回到事件循环，触发这个事件。如果给异常添加了监视器，默认的操作（打印堆栈跟踪信息并退出）就不会发生。                      |
|    Signal 事件    |                                      当进程接收到信号时就触发。信号列表详见标准的 POSIX 信号名，如 SIGINT、SIGUSR1 等。                                      |

### 退出状态码

| 状态码 |                                                                                    名称&描述                                                                                    |
| :----: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|   1    |                                            Uncaught Fatal Exception ，有未捕获异常，并且没有被域或 uncaughtException 处理函数处理。                                             |
|   2    |                                                                                  Unused，保留                                                                                   |
|   3    |                              Internal JavaScript Parse Error，JavaScript 的源码启动 Node 进程时引起解析错误。非常罕见，仅会在开发 Node 时才会有。                               |
|   4    |                        Internal JavaScript Evaluation Failure，JavaScript 的源码启动 Node 进程，评估时返回函数失败。非常罕见，仅会在开发 Node 时才会有。                        |
|   5    |                                               Fatal Error，V8 里致命的不可恢复的错误。通常会打印到 stderr ，内容为： FATAL ERROR                                                |
|   6    |                                Non-function Internal Exception Handler，未捕获异常，内部异常处理函数不知为何设置为 on-function，并且不能被调用。                                |
|   7    | Internal Exception Handler Run-Time Failure，未捕获的异常， 并且异常处理函数处理时自己抛出了异常。例如，如果 process.on('uncaughtException') 或 domain.on('error') 抛出了异常。 |
|   8    |                                                                                  Unused，保留                                                                                   |
|   9    |                                                          Invalid Argument，可能是给了未知的参数，或者给的参数没有值。                                                           |
|   10   |                              Internal JavaScript Run-Time Failure，JavaScript 的源码启动 Node 进程时抛出错误，非常罕见，仅会在开发 Node 时才会有。                              |
|   12   |                                                Invalid Debug Argument，设置了参数--debug 和/或 --debug-brk，但是选择了错误端口。                                                |
|  128   |                  Signal Exits，如果 Node 接收到致命信号，比如 SIGKILL 或 SIGHUP，那么退出代码就是 128 加信号代码。这是标准的 Unix 做法，退出信号代码放在高位。                  |

### process 属性

|    属性    |                                                                 描述                                                                 |
| :--------: | :----------------------------------------------------------------------------------------------------------------------------------: |
|   stdout   |                                                             标准输出流。                                                             |
|   stderr   |                                                             标准错误流。                                                             |
|   stdin    |                                                             标准输入流。                                                             |
|    argv    | argv 属性返回一个数组，由命令行执行脚本时的各个参数组成。它的第一个成员总是 node，第二个成员是脚本文件名，其余成员是脚本文件的参数。 |
|  execPath  |                                            返回执行当前脚本的 Node 二进制文件的绝对路径。                                            |
|  execArgv  |                        返回一个数组，成员是命令行下执行脚本时，在 Node 可执行文件与脚本文件之间的命令行参数。                        |
|    env     |                                              返回一个对象，成员为当前 shell 的环境变量                                               |
|  exitCode  |                               进程退出时的代码，如果进程优通过 process.exit() 退出，不需要指定退出码。                               |
|  version   |                                                     Node 的版本，比如 v0.10.18。                                                     |
|  versions  |                                                 一个属性，包含了 node 的版本和依赖.                                                  |
|   config   |       一个包含用来编译当前 node 执行文件的 javascript 配置选项的对象。它与运行 ./configure 脚本生成的 "config.gypi" 文件相同。       |
|    pid     |                                                          当前进程的进程号。                                                          |
|   title    |                                               进程名，默认值为"node"，可以自定义该值。                                               |
|    arch    |                                             当前 CPU 的架构：'arm'、'ia32' 或者 'x64'。                                              |
|  platform  |                               运行程序所在的平台系统 'darwin', 'freebsd', 'linux', 'sunos' 或 'win32'                                |
| mainModule |   require.main 的备选方法。不同点，如果主模块在运行时改变，require.main 可能会继续返回老的模块。可以认为，这两者引用了同一个模块。   |

### process 方法

|             属性              |                                                           描述                                          |
| :---------------------------: | :-------------------------------------------------------------: | 
|            abort()            |                                                                                                          这将导致 node 触发 abort 事件。会让 node 退出并生成一个核心文件。                                                                                                          |
|       chdir(directory)        |                                                                                                                   改变当前工作进程的目录，如果操作失败抛出异常。                                                                                                                    |
|             cwd()             |                                                                                                                               返回当前进程的工作目录                                                                                                                                |
|         exit([code])          |                                                                                                                使用指定的 code 结束进程。如果忽略，将会使用 code 0。                                                                                                                |
|           getgid()            |                                                                    获取进程的群组标识（参见 getgid(2)）。获取到得时群组的数字 id，而不是名字。注意：这个函数仅在 POSIX 平台上可用(例如，非 Windows 和 Android)。                                                                    |
|          setgid(id)           |                                                        设置进程的群组标识（参见 setgid(2)）。可以接收数字 ID 或者群组名。如果指定了群组名，会阻塞等待解析为数字 ID 。注意：这个函数仅在 POSIX 平台上可用(例如，非 Windows 和                                                        | Android)。 |
|           getuid()            |                                                                        获取进程的用户标识(参见 getuid(2))。这是数字的用户 id，不是用户名。注意：这个函数仅在 POSIX 平台上可用(例如，非 Windows 和 Android)。                                                                        |
|          setuid(id)           |                                                    设置进程的用户标识（参见 setuid(2)）。接收数字 ID 或字符串名字。果指定了群组名，会阻塞等待解析为数字 ID 。注意：这个函数仅在 POSIX 平台上可用(例如，非 Windows 和 Android)。                                                     |
|          getgroups()          |                                                                      返回进程的群组 iD 数组。POSIX 系统没有保证一定有，但是 node.js 保证有。注意：这个函数仅在 POSIX 平台上可用(例如，非 Windows 和 Android)。                                                                      |
|       setgroups(groups)       |                                                                 设置进程的群组 ID。这是授权操作，所以你需要有 root 权限，或者有 CAP_SETGID 能力。注意：这个函数仅在 POSIX 平台上可用(例如，非 Windows 和 Android)。                                                                 |
| initgroups(user, extra_group) |                                          读取 /etc/group ，并初始化群组访问列表，使用成员所在的所有群组。这是授权操作，所以你需要有 root 权限，或者有 CAP_SETGID 能力。注意：这个函数仅在 POSIX 平台上可用(例如，非 Windows 和 Android)。                                           |
|      kill(pid[, signal])      |                                                                   发送信号给进程. pid 是进程 id，并且 signal 是发送的信号的字符串描述。信号名是字符串，比如 'SIGINT' 或 'SIGHUP'。如果忽略，信号会是 'SIGTERM'。                                                                    |
|         memoryUsage()         |                                                                                                             返回一个对象，描述了 Node 进程所用的内存状况，单位为字节。                                                                                                              |
|      nextTick(callback)       |                                                                                                                        一旦当前事件循环结束，调用回调函数。                                                                                                                         |
|         umask([mask])         |                                                                                      设置或读取进程文件的掩码。子进程从父进程继承掩码。如果 mask 参数有效，返回旧的掩码。否则，返回当前掩码。                                                                                       |
|           uptime()            |                                                                                                                             返回 Node 已经运行的秒数。                                                                                                                              |
|           hrtime()            | 返回当前进程的高分辨时间，形式为 [seconds, nanoseconds]数组。它是相对于过去的任意事件。该值与日期无关，因此不受时钟漂移的影响。主要用途是可以通过精确的时间间隔，来衡量程序的性能。你可以将之前的结果传递给当前的 process.hrtime() ，会返回两者间的时间差，用来基准和测量时间间隔。 |

# Node.js 常用工具

util 是一个 Node.js 核心模块，提供常用函数的集合，用于弥补核心 JavaScript 的功能 过于精简的不足。

## util.callbackify

util.callbackify(original) 将 async 异步函数（或者一个返回值为 Promise 的函数）转换成遵循异常优先的回调风格的函数，例如将 (err, value) => ... 回调作为最后一个参数。 在回调函数中，第一个参数为拒绝的原因（如果 Promise 解决，则为 null），第二个参数则是解决的值。

```js
const util = require('util');
async function fn() {
  return 'hello world';
}
const callbackFunction = util.callbackify(fn);
callbackFunction((err, ret) => {
  if (err) throw err;
  console.log(ret);
});
// 输出：hello world
```

## util.inherits

util.inherits(constructor, superConstructor) 是一个实现对象间原型继承的函数。

JavaScript 的面向对象特性是基于原型的，与常见的基于类的不同。JavaScript 没有提供对象继承的语言级别特性，而是通过原型复制来实现的。

## util.inspect

util.inspect(object,[showHidden],[depth],[colors]) 是一个将任意对象转换 为字符串的方法，通常用于调试和错误输出。它至少接受一个参数 object，即要转换的对象。

showHidden 是一个可选参数，如果值为 true，将会输出更多隐藏信息。

depth 表示最大递归的层数，如果对象很复杂，你可以指定层数以控制输出信息的多 少。如果不指定 depth，默认会递归 2 层，指定为 null 表示将不限递归层数完整遍历对象。 如果 colors 值为 true，输出格式将会以 ANSI 颜色编码，通常用于在终端显示更漂亮 的效果。

## util.isArray(object)

如果给定的参数 "object" 是一个数组返回 true，否则返回 false。

## util.isRegExp(object)

如果给定的参数 "object" 是一个正则表达式返回 true，否则返回 false。

## util.isDate(object)

如果给定的参数 "object" 是一个日期返回 true，否则返回 false。

# Node.js 文件系统

Node.js 提供一组类似 UNIX（POSIX）标准的文件操作 API。

## 异步和同步

Node.js 文件系统（fs 模块）模块中的方法均有异步和同步版本，例如读取文件内容的函数有异步的 fs.readFile() 和同步的 fs.readFileSync()。

异步的方法函数最后一个参数为回调函数，回调函数的第一个参数包含了错误信息(error)。

### 实例

```js
// input.txt
文件读取实例;

// main.js
var fs = require('fs');

// 异步
fs.readFile('./input.txt', function (err, res) {
  if (err) {
    return console.log(err);
  }
  console.log('异步读取：' + res.toString());
});

// 同步
var res = fs.readFileSync('./input.txt');
console.log('同步读取： ' + res.toString());
```

## 打开文件

### 语法

```js
fs.open(path, flags[, mode], callback)
```

### 参数说明

- **path** - 文件的路径。
- **flags** - 文件打开的行为。具体值详见下文。
- **mode** - 设置文件模式(权限)，文件创建默认权限为 0666(可读，可写)。
- **callback** - 回调函数，带有两个参数如：callback(err, fd)。

flags 参数对照：
| Flag | 描述 |
|:--:|:--:|
| r |以读取模式打开文件。如果文件不存在抛出异常。|
| r+ | 以读写模式打开文件。如果文件不存在抛出异常。|
| rs | 以同步的方式读取文件。|
| rs+ |以同步的方式读取和写入文件。|
| w |以写入模式打开文件，如果文件不存在则创建。|
| wx | 类似 'w'，但是如果文件路径存在，则文件写入失败。|
| w+ |以读写模式打开文件，如果文件不存在则创建。|
| wx+ | 类似 'w+'， 但是如果文件路径存在，则文件读写失败。|
| a |以追加模式打开文件，如果文件不存在则创建。|
| ax | 类似 'a'， 但是如果文件路径存在，则文件追加失败。|
| a+ | 以读取追加模式打开文件，如果文件不存在则创建。|
| ax+ | 类似 'a+'， 但是如果文件路径存在，则文件读取追加失败。|

## 获取文件信息

### 语法

```js
fs.stat(path, callback);
```

### 参数

- **path** - 文件路径。
- **callback** - 回调函数，带有两个参数如：(err, stats), stats 是 fs.Stats 对象。

stats 类方法:

|           方法            |                                       描述                                        |
| :-----------------------: | :-------------------------------------------------------------------------------: |
|      stats.isFile()       |                       如果是文件返回 true，否则返回 false。                       |
|    stats.isDirectory()    |                       如果是目录返回 true，否则返回 false。                       |
|   stats.isBlockDevice()   |                      如果是块设备返回 true，否则返回 false。                      |
| stats.isCharacterDevice() |                     如果是字符设备返回 true，否则返回 false。                     |
|  stats.isSymbolicLink()   |                      如果是软链接返回 true，否则返回 false。                      |
|      stats.isFIFO()       | 如果是 FIFO，返回 true，否则返回 false。FIFO 是 UNIX 中的一种特殊类型的命令管道。 |
|     stats.isSocket()      |                     如果是 Socket 返回 true，否则返回 false。                     |

## 写入文件

### 语法

```js
fs.writeFile(file, data[, options], callback)
```

### 参数

- **file** - 文件名或文件描述符。
- **data** - 要写入文件的数据，可以是 String(字符串) 或 Buffer(缓冲) 对象。
- **options** - 该参数是一个对象，包含 {encoding, mode, flag}。默认编码为 utf8, 模式为 0666 ， flag 为 'w'
- **callback** - 回调函数，回调函数只包含错误信息参数(err)，在写入失败时返回。

## 读取文件

### 语法

```js
fs.read(fd, buffer, offset, length, position, callback);
```

### 参数

- **fd** - 通过 fs.open() 方法返回的文件描述符。
- **buffer** - 数据写入的缓冲区。
- **offset** - 缓冲区写入的写入偏移量。
- **length** - 要从文件中读取的字节数。
- **position** - 文件读取的起始位置，如果 position 的值为 null，则会从当前文件指针的位置读取。
- **callback** - 回调函数，有三个参数 err, bytesRead, buffer，err 为错误信息， bytesRead 表示读取的字节数，buffer 为缓冲区对象。

## 关闭文件

### 语法

```js
fs.close(fd, callback);
```

### 参数

- **fd** - 通过 fs.open() 方法返回的文件描述符。
- **callback** - 回调函数，没有参数。

## 截取文件

### 语法

```js
fs.ftruncate(fd, len, callback);
```

### 参数

- **fd** - 通过 fs.open() 方法返回的文件描述符。
- **len** - 文件内容截取的长度。
- **callback** - 回调函数，没有参数。

## 删除文件

### 语法

```js
fs.unlink(path, callback);
```

### 参数

- **path** - 文件路径。
- **callback** - 回调函数，没有参数。

## 创建目录

### 语法

```js
fs.mkdir(path[, options], callback)
```

### 参数

- **path** - 文件路径。
- **options** 参数可以是：
  - **recursive** - 是否以递归的方式创建目录，默认为 false。
  - **mode** - 设置目录权限，默认为 0777。
- **callback** - 回调函数，没有参数。

## 读取目录

### 语法

```js
fs.readdir(path, callback);
```

### 参数

- **path** - 文件路径。
- **callback** - 回调函数，回调函数带有两个参数 err, files，err 为错误信息，files 为 目录下的文件数组列表。

## 删除目录

### 语法

```js
fs.rmdir(path, callback);
```

### 参数

- **path** - 文件路径。
- **callback** - 回调函数，没有参数。

## 文件模块方法参考手册

|                            方法                            |                                    描述                                     |
| :--------------------------------------------------------: | :-------------------------------------------------------------------------: |
|           fs.rename(oldPath, newPath, callback)            |              异步 rename().回调函数没有参数，但可能抛出异常。               |
|              fs.ftruncate(fd, len, callback)               |             异步 ftruncate().回调函数没有参数，但可能抛出异常。             |
|                 fs.ftruncateSync(fd, len)                  |                              同步 ftruncate()                               |
|              fs.truncate(path, len, callback)              |             异步 truncate().回调函数没有参数，但可能抛出异常。              |
|                 fs.truncateSync(path, len)                 |                               同步 truncate()                               |
|             fs.chown(path, uid, gid, callback)             |               异步 chown().回调函数没有参数，但可能抛出异常。               |
|                fs.chownSync(path, uid, gid)                |                                同步 chown()                                 |
|             fs.fchown(fd, uid, gid, callback)              |              异步 fchown().回调函数没有参数，但可能抛出异常。               |
|                fs.fchownSync(fd, uid, gid)                 |                                同步 fchown()                                |
|            fs.lchown(path, uid, gid, callback)             |              异步 lchown().回调函数没有参数，但可能抛出异常。               |
|               fs.lchownSync(path, uid, gid)                |                                同步 lchown()                                |
|               fs.chmod(path, mode, callback)               |               异步 chmod().回调函数没有参数，但可能抛出异常。               |
|                  fs.chmodSync(path, mode)                  |                                同步 chmod().                                |
|               fs.fchmod(fd, mode, callback)                |              异步 fchmod().回调函数没有参数，但可能抛出异常。               |
|                  fs.fchmodSync(fd, mode)                   |                               同步 fchmod().                                |
|              fs.lchmod(path, mode, callback)               | 异步 lchmod().回调函数没有参数，但可能抛出异常。Only available on Mac OS X. |
|                 fs.lchmodSync(path, mode)                  |                               同步 lchmod().                                |
|                  fs.stat(path, callback)                   |    异步 stat(). 回调函数有两个参数 err, stats，stats 是 fs.Stats 对象。     |
|                  fs.lstat(path, callback)                  |    异步 lstat(). 回调函数有两个参数 err, stats，stats 是 fs.Stats 对象。    |
|                   fs.fstat(fd, callback)                   |    异步 fstat(). 回调函数有两个参数 err, stats，stats 是 fs.Stats 对象。    |
|                     fs.statSync(path)                      |                     同步 stat(). 返回 fs.Stats 的实例。                     |
|                     fs.lstatSync(path)                     |                    同步 lstat(). 返回 fs.Stats 的实例。                     |
|                      fs.fstatSync(fd)                      |                    同步 fstat(). 返回 fs.Stats 的实例。                     |
|            fs.link(srcpath, dstpath, callback)             |               异步 link().回调函数没有参数，但可能抛出异常。                |
|               fs.linkSync(srcpath, dstpath)                |                                同步 link().                                 |
|       fs.symlink(srcpath, dstpath[, type], callback)       |              异步 symlink().回调函数没有参数，但可能抛出异常。              | type 参数可以设置为 'dir', 'file', 或 'junction' (默认为 'file') 。 |
|          fs.symlinkSync(srcpath, dstpath[, type])          |                               同步 symlink().                               |
|                fs.readlink(path, callback)                 |            异步 readlink(). 回调函数有两个参数 err, linkString。            |
|            fs.realpath(path[, cache], callback)            |           异步 realpath(). 回调函数有两个参数 err, resolvedPath。           |
|               fs.realpathSync(path[, cache])               |                       同步 realpath()。返回绝对路径。                       |
|                 fs.unlink(path, callback)                  |              异步 unlink().回调函数没有参数，但可能抛出异常。               |
|                    fs.unlinkSync(path)                     |                               同步 unlink().                                |
|                  fs.rmdir(path, callback)                  |               异步 rmdir().回调函数没有参数，但可能抛出异常。               |
|                     fs.rmdirSync(path)                     |                                同步 rmdir().                                |
|              fs.mkdir(path[, mode], callback)              |  S 异步 mkdir(2).回调函数没有参数，但可能抛出异常。 访问权限默认为 0777。   |
|                 fs.mkdirSync(path[, mode])                 |                                同步 mkdir().                                |
|                 fs.readdir(path, callback)                 |                      异步 readdir(3). 读取目录的内容。                      |
|                    fs.readdirSync(path)                    |                      同步 readdir().返回文件数组列表。                      |
|                   fs.close(fd, callback)                   |               异步 close().回调函数没有参数，但可能抛出异常。               |
|                      fs.closeSync(fd)                      |                                同步 close().                                |
|           fs.open(path, flags[, mode], callback)           |                               异步打开文件。                                |
|              fs.openSync(path, flags[, mode])              |                         同步 version of fs.open().                          |
|          fs.utimes(path, atime, mtime, callback)           |                                     无                                      |
|             fs.utimesSync(path, atime, mtime)              |                  修改文件时间戳，文件通过指定的文件路径。                   |
|           fs.futimes(fd, atime, mtime, callback)           |                                     无                                      |
|              fs.futimesSync(fd, atime, mtime)              |                    修改文件时间戳，通过文件描述符指定。                     |
|                   fs.fsync(fd, callback)                   |                异步 fsync.回调函数没有参数，但可能抛出异常。                |
|                      fs.fsyncSync(fd)                      |                                 同步 fsync.                                 |
| fs.write(fd, buffer, offset, length[, position], callback) |                将缓冲区内容写入到通过文件描述符指定的文件。                 |
|    fs.write(fd, data[, position[, encoding]], callback)    |                      通过文件描述符 fd 写入文件内容。                       |
|    fs.writeSync(fd, buffer, offset, length[, position])    |                            同步版的 fs.write()。                            |
|       fs.writeSync(fd, data[, position[, encoding]])       |                            同步版的 fs.write().                             |
|  fs.read(fd, buffer, offset, length, position, callback)   |                      通过文件描述符 fd 读取文件内容。                       |
|     fs.readSync(fd, buffer, offset, length, position)      |                              同步版的 fs.read.                              |
|         fs.readFile(filename[, options], callback)         |                             异步读取文件内容。                              |
|            fs.readFileSync(filename[, options])            |                                     无                                      |
|     fs.writeFile(filename, data[, options], callback)      |                             异步写入文件内容。                              |
|        fs.writeFileSync(filename, data[, options])         |                           同步版的 fs.writeFile。                           |
|     fs.appendFile(filename, data[, options], callback)     |                             异步追加文件内容。                              |
|        fs.appendFileSync(filename, data[, options])        |                     The 同步 version of fs.appendFile.                      |
|        fs.watchFile(filename[, options], listener)         |                              查看文件的修改。                               |
|            fs.unwatchFile(filename[, listener])            |                         停止查看 filename 的修改。                          |
|         fs.watch(filename[, options][, listener])          |  查看 filename 的修改，filename 可以是文件或目录。返回 fs.FSWatcher 对象。  |
|                 fs.exists(path, callback)                  |                          检测给定的路径是否存在。                           |
|                    fs.existsSync(path)                     |                             同步版的 fs.exists.                             |
|             fs.access(path[, mode], callback)              |                           测试指定路径用户权限。                            |
|                fs.accessSync(path[, mode])                 |                            同步版的 fs.access。                             |
|            fs.createReadStream(path[, options])            |                           返回 ReadStream 对象。                            |
|           fs.createWriteStream(path[, options])            |                           返回 WriteStream 对象。                           |
|       fs.symlink(srcpath, dstpath[, type], callback)       |              异步 symlink().回调函数没有参数，但可能抛出异常。              |

# Node.js GET/POST 请求

在很多场景中，我们的服务器都需要跟用户的浏览器打交道，如表单提交。

表单提交到服务器一般都使用 GET/POST 请求。

## 获取 GET 请求内容

由于 GET 请求直接被嵌入在路径中，URL 是完整的请求路径，包括了?后面的部分，所以可以直接获取 URL 并通过简单的解析，即可获得请求参数。

```js
var http = require('http');
var url = require('url');
var util = require('util');

http
  .createServer(function (req, res) {
    res.writeHead(200, { 'Content-type': 'text/plain; charset=utf-8' });
    res.end(util.inspect(url.parse(req.url, true)));
  })
  .listen(8888);
```

浏览器中访问的地址：http://localhost:8888/index?user=xiaozhang&url=www.baidu.com

![Snipaste_2021-05-19_14-42-35.png](https://i.loli.net/2021/05/19/ARLGMzdlqrV14t3.png)

其中， util.inspect(url.parse(req.url, true)).query 返回的是 url 中的参数对象。

## 获取 POST 请求内容

POST 请求的内容全部的都在请求体中，http.ServerRequest 并没有一个属性内容为请求体，原因是等待请求体传输可能是一件耗时的工作。

比如上传文件，而很多时候我们可能并不需要理会请求体的内容，恶意的 POST 请求会大大消耗服务器的资源，所以 node.js 默认是不会解析请求体的，当需要的时候，需要手动来做。

```js
var http = require('http');
var querystring = require('querystring');

var postHTML =
  '<html><head><meta charset="utf-8"></head>' +
  '<body>' +
  '<form method="post">' +
  '网站名： <input name="name"><br>' +
  '网站 URL： <input name="url"><br>' +
  '<input type="submit">' +
  '</form>' +
  '</body></html>';

http
  .createServer(function (req, res) {
    var body = '';
    req.on('data', function (chunk) {
      body += chunk;
    });
    req.on('end', function () {
      // 解析参数
      body = querystring.parse(body);
      // 设置响应头部信息及编码
      res.writeHead(200, { 'Content-Type': 'text/html; charset=utf8' });

      if (body.name && body.url) {
        // 输出提交的数据
        res.write('网站名：' + body.name);
        res.write('<br>');
        res.write('网站 URL：' + body.url);
      } else {
        // 输出表单
        res.write(postHTML);
      }
      res.end();
    });
  })
  .listen(3000);
```

# Node.js 工具模块

## 常用的模块

|   模块名    |                            描述                             |
| :---------: | :---------------------------------------------------------: |
|   OS 模块   |                  提供基本的系统操作函数。                   |
|  Path 模块  |              提供了处理和转换文件路径的工具。               |
|  Net 模块   |     用于底层的网络通信。提供了服务端和客户端的的操作。      |
|  DNS 模块   |                       用于解析域名。                        |
| Domain 模块 | 简化异步代码的异常处理，可以捕捉处理 try catch 无法捕捉的。 |

## OS 模块

Node.js os 模块提供了一些基本的系统操作函数。

### 方法

|         方法名         |                                                                          描述                                                                          |
| :--------------------: | :-----------------------------------------------------------------------------------------------------------------: |
|      os.tmpdir()       |                                                             返回操作系统的默认临时文件夹。                                                             |
|    os.endianness()     |                                                       返回 CPU 的字节序，可能的是 "BE" 或 "LE"。                                                       |
|     os.hostname()      |                                                                 返回操作系统的主机名。                                                                 |
|       os.type()        |                                                                     返回操作系统名                                                                     |
|     os.platform()      |                                                                 返回编译时的操作系统名                                                                 |
|       os.arch()        |                                               返回操作系统 CPU 架构，可能的值有 "x64"、"arm" 和 "ia32"。                                               |
|      os.release()      |                                                                返回操作系统的发行版本。                                                                |
|      os.uptime()       |                                                          返回操作系统运行的时间，以秒为单位。                                                          |
|      os.loadavg()      |                                                       返回一个包含 1、5、15 分钟平均负载的数组。                                                       |
|     os.totalmem()      |                                                             返回系统内存总量，单位为字节。                                                             |
|      os.freemem()      |                                                          返回操作系统空闲内存量，单位是字节。                                                          |
|       os.cpus()        | 返回一个对象数组，包含所安装的每个 CPU/内核的信息：型号、速度（单位 MHz）、时间（一个包含 user、nice、sys、idle 和 irq 所使用 CPU/内核毫秒数的对象）。 |
| os.networkInterfaces() |                                                                   获得网络接口列表。                                                                   |

### 属性

| 属性名 |              描述              |
| :----: | :----------------------------: |
| os.EOL | 定义了操作系统的行尾符的常量。 |

## Path 模块

Node.js path 模块提供了一些用于处理文件路径的小工具。

### 方法

|               方法名               |                                                                                                              描述                                                                                                              |
| :--------------------------------: | :---------------------------------------------------------------------: |
|         path.normalize(p)          |                                                                                                 规范化路径，注意'..' 和 '.'。                                                                                                  |
| path.join([path1][, path2][, ...]) |                                                            用于连接路径。该方法的主要用途在于，会正确使用当前系统的路径分隔符，Unix 系统是"/"，Windows 系统是"\"。                                                             |
|    path.resolve([from ...], to)    | 将 to 参数解析为绝对路径，给定的路径的序列是从右往左被处理的，后面每个 path 被依次解析，直到构造完成一个绝对路径。 例如，给定的路径片段的序列为：/foo、/bar、baz，则调用 path.resolve('/foo', '/bar', 'baz') 会返回 /bar/baz。 |
|       path.isAbsolute(path)        |                                                                                                 判断参数 path 是否是绝对路径。                                                                                                 |
|      path.relative(from, to)       |                                                                         用于将绝对路径转为相对路径，返回从 from 到 to 的相对路径（基于当前工作目录）。                                                                         |
|          path.dirname(p)           |                                                                                   返回路径中代表文件夹的部分，同 Unix 的 dirname 命令类似。                                                                                    |
|      path.basename(p[, ext])       |                                                                                      返回路径中的最后一部分。同 Unix 命令 bashname 类似。                                                                                      |
|          path.extname(p)           |                                   返回路径中文件的后缀名，即路径中最后一个'.'之后的部分。如果一个路径中并不包含'.'或该路径只包含一个'.' 且这个'.'为路径的第一个字符，则此命令返回空字符串。                                    |
|       path.parse(pathString)       |                                                                                                     返回路径字符串的对象。                                                                                                     |
|      path.format(pathObject)       |                                                                                          从对象中返回路径字符串，和 path.parse 相反。                                                                                          |

### 属性

|     属性名     |                          描述                           |
| :------------: | :-----------------------------------------------------: |
|    path.sep    |           平台的文件路径分隔符，'\\' 或 '/'。           |
| path.delimiter |                 平台的分隔符, ; or ':'.                 |
|   path.posix   | 提供上述 path 的方法，不过总是以 posix 兼容的方式交互。 |
|   path.win32   | 提供上述 path 的方法，不过总是以 win32 兼容的方式交互。 |

## Net 模块

Node.js Net 模块提供了一些用于底层的网络通信的小工具，包含了创建服务器/客户端的方法。

### 方法

|                        方法名                         |                                                                          描述                                                                          |
| :---------------------------------------------------: | :---------------------------------------------------------------------------------: |
|   net.createServer([options][, connectionlistener])   |                                   创建一个 TCP 服务器。参数 connectionListener 自动给 'connection' 事件创建监听器。                                    |
|      net.connect(options[, connectionListener])       |                                                 返回一个新的 'net.Socket'，并连接到指定的地址和端口。                                                  |
|    当 socket 建立的时候，将会触发 'connect' 事件。    |
|  net.createConnection(options[, connectionListener])  |                                        创建一个到端口 port 和 主机 host 的 TCP 连接。 host 默认为 'localhost'。                                        |
|     net.connect(port[, host][, connectlistener])      | 创建一个端口为 port 和主机为 host 的 TCP 连接 。host 默认为 'localhost'。参数 connectListener 将会作为监听器添加到 'connect' 事件。返回 'net.Socket'。 |
| net.createConnection(port[, host][, connectlistener]) | 创建一个端口为 port 和主机为 host 的 TCP 连接 。host 默认为 'localhost'。参数 connectListener 将会作为监听器添加到 'connect' 事件。返回 'net.Socket'。 |
|         net.connect(path[, connectListener])          |                    创建连接到 path 的 unix socket 。参数 connectListener 将会作为监听器添加到 'connect' 事件上。返回 'net.Socket'。                    |
|     net.createConnection(path[, connectListener])     |                     创建连接到 path 的 unix socket 。参数 connectListener 将会作为监听器添加到 'connect' 事件。返回 'net.Socket'。                     |
|                    net.isIP(input)                    |                                         检测输入的是否为 IP 地址。 IPV4 返回 4， IPV6 返回 6，其他情况返回 0。                                         |
|                   net.isIPv4(input)                   |                                                  如果输入的地址为 IPV4， 返回 true，否则返回 false。                                                   |
|                   net.isIPv6(input)                   |                                                  如果输入的地址为 IPV6， 返回 true，否则返回 false。                                                   |

### net.Server

net.Server 通常用于创建一个 TCP 或本地服务器。

#### 方法：

|                       方法名                       |                                                                                            描述                                                                                             |
| :------------------------------------------------: | :----------------------------------------------------------------------------------------: |
| server.listen(port[, host][, backlog][, callback]) |                        监听指定端口 port 和 主机 host ac 连接。 默认情况下 host 接受任何 IPv4 地址(INADDR_ANY)的直接连接。端口 port 为 0 时，则会分配一个随机端口。                         |
|          server.listen(path[, callback])           |                                                                     通过指定 path 的连接，启动一个本地 socket 服务器。                                                                      |
|         server.listen(handle[, callback])          |                                                                                     通过指定句柄连接。                                                                                      |
|         server.listen(options[, callback])         | options 的属性：端口 port, 主机 host, 和 backlog, 以及可选参数 callback 函数, 他们在一起调用 server.listen(port, [host], [backlog], [callback])。还有，参数 path 可以用来指定 UNIX socket。 |
|              server.close([callback])              |                                        服务器停止接收新的连接，保持现有连接。这是异步函数，当所有连接结束的时候服务器会关闭，并会触发 'close' 事件。                                        |
|                  server.address()                  |                                                                       操作系统返回绑定的地址，协议族名和服务器端口。                                                                        |
|                   server.unref()                   |                                                             如果这是事件系统中唯一一个活动的服务器，调用 unref 将允许程序退出。                                                             |
|                    server.ref()                    |                与 unref 相反，如果这是唯一的服务器，在之前被 unref 了的服务器上调用 ref 将不会让程序退出（默认行为）。如果服务器已经被 ref，则再次调用 ref 并不会产生影响。                 |
|          server.getConnections(callback)           |                                            异步获取服务器当前活跃连接的数量。当 socket 发送给子进程后才有效；回调函数有 2 个参数 err 和 count。                                             |

#### 事件：

|   事件名   |                                      描述                                      |
| :--------: | :----------------------------------------------------------------------------: |
| listening  |                   当服务器调用 server.listen 绑定后会触发。                    |
| connection |              当新连接创建后会被触发。socket 是 net.Socket 实例。               |
|   close    | 服务器关闭时会触发。注意，如果存在连接，这个事件不会被触发直到所有的连接关闭。 |
|   error    |               发生错误时触发。'close' 事件将被下列事件直接调用。               |

### net.Socket

net.Socket 对象是 TCP 或 UNIX Socket 的抽象。net.Socket 实例实现了一个双工流接口。 他们可以在用户创建客户端(使用 connect())时使用, 或者由 Node 创建它们，并通过 connection 服务器事件传递给用户。

#### 事件

| 事件名  |                                            描述                                             |
| :-----: | :-----------------------------------------------------------------------------------------: |
| lookup  |               在解析域名后，但在连接前，触发这个事件。对 UNIX sokcet 不适用。               |
| connect |                                成功建立 socket 连接时触发。                                 |
|  data   |                                    当接收到数据时触发。                                     |
|   end   |                         当 socket 另一端发送 FIN 包时，触发该事件。                         |
| timeout |         当 socket 空闲超时时触发，仅是表明 socket 已经空闲。用户必须手动关闭连接。          |
|  drain  |                          当写缓存为空得时候触发。可用来控制上传。                           |
|  error  |                                      错误发生时触发。                                       |
|  close  | 当 socket 完全关闭时触发。参数 had_error 是布尔值，它表示是否因为传输错误导致 socket 关闭。 |

#### 属性

|        属性名        |                                                                           描述                                                                            |
| :------------------: | :----------------------------------------------------------------------------------------: |
|  socket.bufferSize   |                                                            该属性显示了要写入缓冲区的字节数。                                                             |
| socket.remoteAddress |                                          远程的 IP 地址字符串，例如：'74.125.127.100' or '2001:4860:a005::68'。                                           |
| socket.remoteFamily  |                                                       远程 IP 协议族字符串，比如 'IPv4' or 'IPv6'。                                                       |
|  socket.remotePort   |                                                           远程端口，数字表示，例如：80 or 21。                                                            |
| socket.localAddress  | 网络连接绑定的本地接口 远程客户端正在连接的本地 IP 地址，字符串表示。例如，如果你在监听'0.0.0.0'而客户端连接在'192.168.1.1'，这个值就会是 '192.168.1.1'。 |
|   socket.localPort   |                                                         本地端口地址，数字表示。例如：80 or 21。                                                          |
|   socket.bytesRead   |                                                                     接收到得字节数。                                                                      |
| socket.bytesWritten  |                                                                      发送的字节数。                                                                       |

#### 方法

|                     方法名                      |                                                                                                                                描述                                                                                                                                 |
| :---------------------------------------------: | :---------------------------------------------------------------------------------: |
|            new net.Socket([options])            |                                                                                                                     构造一个新的 socket 对象。                                                                                                                      |
| socket.connect(port[, host][, connectlistener]) |                                               指定端口 port 和 主机 host，创建 socket 连接 。参数 host 默认为 localhost。通常情况不需要使用 net.createConnection 打开 socket。只有你实现了自己的 socket 时才会用到。                                                |
|     socket.connect(path[, connectListener])     |                                                                       打开指定路径的 unix socket。通常情况不需要使用 net.createConnection 打开 socket。只有你实现了自己的 socket 时才会用到。                                                                       |
|         socket.setEncoding([encoding])          |                                                                                                                              设置编码                                                                                                                               |
|   socket.write(data[, encoding][, callback])    |                                                                                               在 socket 上发送数据。第二个参数指定了字符串的编码，默认是 UTF8 编码。                                                                                                |
|         socket.end([data][, encoding])          |                                                                                                  半关闭 socket。例如，它发送一个 FIN 包。可能服务器仍在发送数据。                                                                                                   |
|                socket.destroy()                 |                                                                                           确保没有 I/O 活动在这个套接字上。只有在错误发生情况下才需要。（处理错误等等）。                                                                                           |
|                 socket.pause()                  |                                                                                                 暂停读取数据。就是说，不会再触发 data 事件。对于控制上传非常有用。                                                                                                  |
|                 socket.resume()                 |                                                                                                                   调用 pause() 后想恢复读取数据。                                                                                                                   |
|     socket.setTimeout(timeout[, callback])      |                                                                                                     socket 闲置时间超过 timeout 毫秒后 ，将 socket 设置为超时。                                                                                                     |
|          socket.setNoDelay([noDelay])           |                                              禁用纳格（Nagle）算法。默认情况下 TCP 连接使用纳格算法，在发送前他们会缓冲数据。将 noDelay 设置为 true 将会在调用 socket.write() 时立即发送数据。noDelay 默认值为 true。                                               |
|  socket.setKeepAlive([enable][, initialdelay])  | 禁用/启用长连接功能，并在发送第一个在闲置 socket 上的长连接 probe 之前，可选地设定初始延时。默认为 false。 设定 initialDelay （毫秒），来设定收到的最后一个数据包和第一个长连接 probe 之间的延时。将 initialDelay 设为 0，将会保留默认（或者之前）的值。默认值为 0. |
|                socket.address()                 |                                                                  操作系统返回绑定的地址，协议族名和服务器端口。返回的对象有 3 个属性，比如{ port: 12346, family: 'IPv4', address: '127.0.0.1' }。                                                                   |
|                 socket.unref()                  |                                                                     如果这是事件系统中唯一一个活动的服务器，调用 unref 将允许程序退出。如果服务器已被 unref，则再次调用 unref 并不会产生影响。                                                                      |
|                  socket.ref()                   |                                                    与 unref 相反，如果这是唯一的服务器，在之前被 unref 了的服务器上调用 ref 将不会让程序退出（默认行为）。如果服务器已经被 ref，则再次调用 ref 并不会产生影响。                                                     |

## DNS 模块

Node.js DNS 模块用于解析域名。

### 方法

|                   方法名                   |                                                                                                                                        描述                                                                                                                                        |
| :----------------------------------------: | :---------------------------------------------------------------------------------------------: |
| dns.lookup(hostname[, options], callback)  |                                         将域名（比如 'runoob.com'）解析为第一条找到的记录 A （IPV4）或 AAAA(IPV6)。参数 options 可以是一个对象或整数。如果没有提供 options，IP v4 和 v6 地址都可以。如果 options 是整数，则必须是 4 或 6。                                         |
| dns.lookupService(address, port, callback) |                                                                                                                使用 getnameinfo 解析传入的地址和端口为域名和服务。                                                                                                                 |
| dns.resolve(hostname[, rrtype], callback)  |                                                                                                        将一个域名（如 'runoob.com'）解析为一个 rrtype 指定记录类型的数组。                                                                                                         |
|      dns.resolve4(hostname, callback)      |                                                                      和 dns.resolve() 类似, 仅能查询 IPv4 (A 记录）。 addresses IPv4 地址数组 (比如，['74.125.79.104', '74.125.79.105', '74.125.79.106']）。                                                                       |
|      dns.resolve6(hostname, callback)      |                                                                                                                和 dns.resolve4() 类似， 仅能查询 IPv6( AAAA 查询）                                                                                                                 |
|     dns.resolveMx(hostname, callback)      |                                                                                                                 和 dns.resolve() 类似, 仅能查询邮件交换(MX 记录)。                                                                                                                 |
|     dns.resolveTxt(hostname, callback)     |                                  和 dns.resolve() 类似, 仅能进行文本查询 (TXT 记录）。 addresses 是 2-d 文本记录数组。(比如，[ ['v=spf1 ip4:0.0.0.0 ', '~all' ] ]）。 每个子数组包含一条记录的 TXT 块。根据使用情况可以连接在一起，也可单独使用。                                  |
|     dns.resolveSrv(hostname, callback)     | 和 dns.resolve() 类似, 仅能进行服务记录查询 (SRV 记录）。 addresses 是 hostname 可用的 SRV 记录数组。 SRV 记录属性有优先级（priority），权重（weight）, 端口（port）, 和名字（name） (比如，[{'priority': 10, 'weight': 5, 'port': 21223, 'name': 'service.example.com'}, ...]）。 |
|     dns.resolveSoa(hostname, callback)     |                                                                                                                和 dns.resolve() 类似, 仅能查询权威记录(SOA 记录）。                                                                                                                |
|     dns.resolveNs(hostname, callback)      |                                                        和 dns.resolve() 类似, 仅能进行域名服务器记录查询(NS 记录）。 addresses 是域名服务器记录数组（hostname 可以使用） (比如, ['ns1.example.com', 'ns2.example.com']）。                                                         |
|    dns.resolveCname(hostname, callback)    |                                                                       和 dns.resolve() 类似, 仅能进行别名记录查询 (CNAME 记录)。addresses 是对 hostname 可用的别名记录数组 (比如，, ['bar.example.com']）。                                                                        |
|         dns.reverse(ip, callback)          |                                                                                                                    反向解析 IP 地址，指向该 IP 地址的域名数组。                                                                                                                    |
|              dns.getServers()              |                                                                                                                    返回一个用于当前解析的 IP 地址数组的字符串。                                                                                                                    |
|          dns.setServers(servers)           |                                                                                                                          指定一组 IP 地址作为解析服务器。                                                                                                                          |

#### rrtypes

dns.resolve() 方法中有效的 rrtypes 值:

- 'A' IPV4 地址, 默认
- 'AAAA' IPV6 地址
- 'MX' 邮件交换记录
- 'TXT' text 记录
- 'SRV' SRV 记录
- 'PTR' 用来反向 IP 查找
- 'NS' 域名服务器记录
- 'CNAME' 别名记录
- 'SOA' 授权记录的初始值

### 错误码

每次 DNS 查询都可能返回以下错误码：

- dns.NODATA: 无数据响应。
- dns.FORMERR: 查询格式错误。
- dns.SERVFAIL: 常规失败。
- dns.NOTFOUND: 没有找到域名。
- dns.NOTIMP: 未实现请求的操作。
- dns.REFUSED: 拒绝查询。
- dns.BADQUERY: 查询格式错误。
- dns.BADNAME: 域名格式错误。
- dns.BADFAMILY: 地址协议不支持。
- dns.BADRESP: 回复格式错误。
- dns.CONNREFUSED: 无法连接到 DNS 服务器。
- dns.TIMEOUT: 连接 DNS 服务器超时。
- dns.EOF: 文件末端。
- dns.FILE: 读文件错误。
- dns.NOMEM: 内存溢出。
- dns.DESTRUCTION: 通道被摧毁。
- dns.BADSTR: 字符串格式错误。
- dns.BADFLAGS: 非法标识符。
- dns.NONAME: 所给主机不是数字。
- dns.BADHINTS: 非法 HINTS 标识符。
- dns.NOTINITIALIZED: c c-ares 库尚未初始化。
- dns.LOADIPHLPAPI: 加载 iphlpapi.dll 出错。
- dns.ADDRGETNETWORKPARAMS: 无法找到 GetNetworkParams 函数。
- dns.CANCELLED: 取消 DNS 查询。

## Domain 模块

Node.js Domain(域) 简化异步代码的异常处理，可以捕捉处理 try catch 无法捕捉的异常。引入 Domain 模块 语法格式如下：

domain 模块，把处理多个不同的 IO 的操作作为一个组。注册事件和回调到 domain，当发生一个错误事件或抛出一个错误时，domain 对象会被通知，不会丢失上下文环境，也不导致程序错误立即退出，与 process.on('uncaughtException')不同。

Domain 模块可分为隐式绑定和显式绑定：

- 隐式绑定: 把在 domain 上下文中定义的变量，自动绑定到 domain 对象
- 显式绑定: 把不是在 domain 上下文中定义的变量，以代码的方式绑定到 domain 对象

### 方法

|           方法名           |                                                           描述                                                            |
| :------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
|    domain.run(function)    |                       在域的上下文运行提供的函数，隐式的绑定了所有的事件分发器，计时器和底层请求。                        |
|    domain.add(emitter)     |                                                      显式的增加事件                                                       |
|   domain.remove(emitter)   |                                                        删除事件。                                                         |
|   domain.bind(callback)    | 返回的函数是一个对于所提供的回调函数的包装函数。当调用这个返回的函数时，所有被抛出的错误都会被导向到这个域的 error 事件。 |
| domain.intercept(callback) |           和 domain.bind(callback) 类似。除了捕捉被抛出的错误外，它还会拦截 Error 对象作为参数传递到这个函数。            |
|       domain.enter()       |                                         进入一个异步调用的上下文，绑定到 domain。                                         |
|       domain.exit()        |                       退出当前的 domain，切换到不同的链的异步调用的上下文中。对应 domain.enter()。                        |
|      domain.dispose()      |                                    释放一个 domain 对象，让 node 进程回收这部分资源。                                     |
|      domain.create()       |                                                  返回一个 domain 对象。                                                   |

### 属性

|     属性名     |                       描述                       |
| :------------: | :----------------------------------------------: |
| domain.members | 已加入 domain 对象的域定时器和事件发射器的数组。 |

# Node.js Web 模块

## 是什么是 Web 服务器

Web 服务器一般指网站服务器，是指驻留于因特网上某种类型计算机的程序，Web 服务器的基本功能就是提供 Web 信息浏览服务。它只需支持 HTTP 协议、HTML 文档格式及 URL，与客户端的网络浏览器配合。

目前最主流的三个 Web 服务器是 Apache、Nginx、IIS。

## Web 应用架构

![image.png](https://i.loli.net/2021/05/21/VlFXRPTakNEet56.png)

- **Client** - 客户端，一般指浏览器，浏览器可以通过 HTTP 协议向服务器请求数据。
- **Server** - 服务端，一般指 Web 服务器，可以接收客户端请求，并向客户端发送响应数据。
- **Business** - 业务层， 通过 Web 服务器处理应用程序，如与数据库交互，逻辑运算，调用外部程序等。
- **Data** - 数据层，一般由数据库组成。

## 使用 Node 创建 Web 服务器

Node.js 提供了 http 模块，http 模块主要用于搭建 HTTP 服务端和客户端，使用 HTTP 服务器或客户端功能必须调用 http 模块。

### 实例

```js
// server.js
var http = require('http'); // web 服务请求模块
var fs = require('fs'); // 文件操作模块
var url = require('url'); // 地址栏操作模块

http
  .createServer(function (request, response) {
    // 获取地址栏中的文件访问，测试地址：http://127.0.0.1:8888/index.html
    var pathname = url.parse(request.url).pathname;
    console.log('Request for ' + pathname + ' received.');

    // 根据文件名找到该文件
    // 注意：参数一的前提是server。js和index。html在同一个目录下
    // 如果不在同一个目录可以适当添加文件路径，如这里我是将server.js放在了与index.html同目录js下的：'../' + pathname.substr(1)
    fs.readFile(pathname.substr(1), function (err, data) {
      // 不存在该文件
      if (err) {
        console.log(err);
        response.writeHead(404, { 'Content-Type': 'text/html' });
      } else {
        // 存在该文件，进行内容读取
        response.writeHead(200, { 'Content-type': 'text/html' });
        response.write(data.toString());
      }

      response.end();
    });
  })
  .listen(8888); // 访问端口号

console.log('Server running at http://127.0.0.1:8888');
```

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>node.js web server</title>
  </head>
  <body>
    <h1>我的第一个标题</h1>
    <p>我的第一个段落。</p>
  </body>
</html>
```

# Node.js Express 框架

## Express 简介

Express 是一个简洁而灵活的 node.js Web应用框架, 提供了一系列强大特性帮助你创建各种 Web 应用，和丰富的 HTTP 工具。

使用 Express 可以快速地搭建一个完整功能的网站。

Express 框架核心特性：
- 可以设置中间件来响应 HTTP 请求。
- 定义了路由表用于执行不同的 HTTP 请求动作。
- 可以通过向模板传递参数来动态渲染 HTML 页面。

## 安装 Express

安装 Express 并将其保存到依赖列表中：

```md
$ cnpm install express --save
```

以上命令会将 Express 框架安装在当前目录的 node_modules 目录中， node_modules 目录下会自动创建 express 目录。以下几个重要的模块是需要与 express 框架一起安装的：

- body-parser - node.js 中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。
- cookie-parser - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。
- multer - node.js 中间件，用于处理 enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。

```md
$ cnpm install body-parser --save
$ cnpm install cookie-parser --save
$ cnpm install multer --save
```

# Node.js RESTful API

## 什么是 REST？
REST即表述性状态传递（英文：Representational State Transfer，简称REST）是Roy Fielding博士在2000年他的博士论文中提出来的一种软件架构风格。

表述性状态转移是一组架构约束条件和原则。满足这些约束条件和原则的应用程序或设计就是RESTful。需要注意的是，REST是设计风格而不是标准。REST通常基于使用HTTP，URI，和XML（标准通用标记语言下的一个子集）以及HTML（标准通用标记语言下的一个应用）这些现有的广泛流行的协议和标准。REST 通常使用 JSON 数据格式。

# Node.js 多进程

是事件驱动来处理并发，这样有助于在多核 cpu 的系统上创建多个子进程，从而提高性能。

每个子进程总是带有三个流对象：child.stdin, child.stdout 和child.stderr。他们可能会共享父进程的 stdio 流，或者也可以是独立的被导流的流对象。

Node 提供了 child_process 模块来创建子进程，方法有：
- exec - child_process.exec 使用子进程执行命令，缓存子进程的输出，并将子进程的输出以回调函数参数的形式返回。
- spawn - child_process.spawn 使用指定的命令行参数创建新进程。
- fork - child_process.fork 是 spawn()的特殊形式，用于在子进程中运行的模块，如 fork('./son.js') 相当于 spawn('node', ['./son.js']) 。与spawn方法不同的是，fork会在父进程与子进程之间，建立一个通信管道，用于进程之间的通信。

# Node.js JXcore 打包
Node.js 是一个开放源代码、跨平台的、用于服务器端和网络应用的运行环境。

JXcore 是一个支持多线程的 Node.js 发行版本，基本不需要对现有的代码做任何改动就可以直接线程安全地以多线程运行。
