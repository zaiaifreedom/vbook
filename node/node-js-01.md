### 第一篇：了解Node.js

### 前言

简单的说 Node.js 就是运行在服务端的 JavaScript。

Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。

Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。



### 创建应用

如果我们使用PHP来编写后端的代码时，需要Apache 或者 Nginx 的HTTP 服务器，并配上 mod_php5 模块和php-cgi。

从这个角度看，整个"接收 HTTP 请求并提供 Web 页面"的需求根本不需 要 PHP 来处理。

不过对 Node.js 来说，概念完全不一样了。使用 Node.js 时，我们不仅仅 在实现一个应用，同时还实现了 **整个 HTTP 服务器**。事实上，我们的 Web 应用以及对应的 Web 服务器基本上是一样的。

我们应用的组成：

1. **引入 required 模块：**我们可以使用 require 指令来载入 Node.js 模块。
2. **创建服务器：**服务器可以监听客户端的请求，类似于 Apache 、Nginx 等 HTTP 服务器。
3. **接收请求与响应请求：** 服务器很容易创建，客户端可以使用浏览器或终端发送 HTTP 请求，服务器接收请求后返回响应数据。



#### 实践

```js
var http = require('http');

http.createServer(function (request, response) {

    // 发送 HTTP 头部 
    // HTTP 状态值: 200 : OK
    // 内容类型: text/plain
    response.writeHead(200, {'Content-Type': 'text/plain'});

    // 发送响应数据 "Hello World"
    response.end('Hello World\n');
}).listen(8888);

// 终端打印如下信息
console.log('Server running at http://127.0.0.1:8888/');
```



**分析Node.js 的 HTTP 服务器：**

- 第一行请求（require）Node.js 自带的 http 模块，并且把它赋值给 http 变量。
- 接下来我们调用 http 模块提供的函数： createServer 。这个函数会返回 一个对象，这个对象有一个叫做 listen 的方法，这个方法有一个数值参数， 指定这个 HTTP 服务器监听的端口号。



### npm 模块

常用的命令——



搜索模块:   `npm search express`

更新模块:  `npm update express`

初始化模块：`npm init`

发布模块：`npm publish`

查看当前文件夹安装的所有模块：`npm list --depth=0`

查看全局安装过的模块： `npm list --depth=0 -global`

清理npm缓存： `npm cache clear`



#### 版本号

使用NPM下载和发布代码时都会接触到版本号。NPM使用语义版本号来管理代码，这里简单介绍一下。 语义版本号分为X.Y.Z三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新。

- 如果只是修复bug，需要更新Z位。
- 如果是新增了功能，但是向下兼容，需要更新Y位。
- 如果有大变动，向下不兼容，需要更新X位。

版本号有了这个保证后，在申明第三方包依赖时，除了可依赖于一个固定版本号外，还可依赖于某个范围的版本号。例如"argv": "0.0.x"表示依赖于0.0.x系列的最新版argv。

NPM支持的所有版本号范围指定方式可以查看[官方文档]。



#### cnpm 

十分钟更新

` npm install -g cnpm --registry=https://registry.npm.taobao.org`



### REPL(交互式解释器)

Node.js REPL(Read Eval Print Loop:交互式解释器) 表示一个电脑的环境，类似 Window 系统的终端或 Unix/Linux shell，我们可以在终端中输入命令，并接收系统的响应。

Node 自带了交互式解释器，可以执行以下任务：

- **读取** - 读取用户输入，解析输入了Javascript 数据结构并存储在内存中。
- **执行** - 执行输入的数据结构
- **打印** - 输出结果
- **循环** - 循环操作以上步骤直到用户两次按下 ctrl-c 按钮退出。

Node 的交互式解释器可以很好的调试 Javascript 代码。



#### 多行表达式

REPL 遇到声明，大括号，小括号会自动进入多行表达式



#### 下划线变量

可以使用下划线(_)获取表达式的运算结果



#### 命令

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



### 回调函数

Node.js 异步编程的直接体现就是回调。

异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。

回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，**Node 所有 API 都支持回调函数** 。

例如，我们可以一边读取文件，一边执行其他命令，在文件读取完成后，我们将文件内容作为回调函数的参数返回。这样在执行代码时就没有阻塞或等待文件 I/O 操作。这就大大提高了 Node.js 的性能，可以处理大量的并发请求。



### 事件循环

Node.js 是单进程单线程应用程序，但是通过 **事件和回调支持并发** ，所以性能非常高。

Node.js 的每一个 API 都是异步的，并作为一个独立线程运行，使用异步函数调用，并处理并发。

Node.js 基本上所有的事件机制都是用设计模式中 **观察者模式** 实现。

Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.



### 事件驱动程序

Node.js 使用事件驱动模型，当web server接收到请求，就把它关闭然后进行处理，然后去服务下一个web请求。

这里 关闭这个 EventEmitters, 不如说是 把这个 EventEmitters 处于挂起状态，再次去执行内部事件，然而内部事件程序的 EventEmitters 又间接地依赖其他的事件处理程序（被其他事件占用主线程就要等），一直往后面执行（维持着作用域 和 this 值），直到 end 关闭这个 EventEmitters。

又或者，不关闭这个 EventEmitters， 因为程序没有在 回调 中结束这个事件，那我在想：它会不会自己在固定的时间内进行清除，同时又不关闭这个服务，这样客户端的结果就是 no reply.  因为关闭这个服务意味着，会立马返回客户端一个 no reply.

![img](https://user-gold-cdn.xitu.io/2016/11/29/95749e5fcb1ff040f4295036d7964aac?imageslim)



整个事件驱动的流程就是这么实现的，非常简洁。有点类似于观察者模式，事件相当于一个主题(Subject)，而所有注册到这个事件上的处理函数相当于观察者(Observer)。

单独这样去理解事件，确实要轻松许多😄

Node.js 有多个内置的事件，我们可以通过引入 events 模块，并通过实例化 EventEmitter 类来绑定和监听事件，如下实例：



```js
// 引入 events 模块
var events = require('events')
// 创建事件主题对象 (单例)
var eventEmitter = new events.EventEmitter();
```

以下程序绑定事件处理程序：

```js
// 绑定事件及事件的处理程序, 注意 eventHandler 是(回调)函数，不是函数执行表达式
eventEmitter.on('eventName', eventHandler)
```

我们可以通过程序触发事件：

```js
eventEmitter.emit('eventName')
```



### Node 应用程序是如何工作的

在 Node 应用程序中，执行异步操作的函数将回调函数作为最后一个参数， 回调函数接收错误对象作为第一个参数。

创建 main.js 文件

```js
var fs = require('fs')

fs.readFile('input.txt', function(err, data) {
  if (err) {
    console.log(err.stack)
    return
  }
  console.log(data.toString())
})
```



### EventEmitter

Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到 **事件队列**。

Node.js里面的许多对象都会分发事件：一个net.Server对象会在每次有新连接时分发一个事件， 一个fs.readStream对象会在文件被打开的时候发出一个事件。 所有这些产生事件的对象都是 events.EventEmitter 的实例。



### EventEmitter 类

events 模块只提供了一个对象： **events.EventEmitter** 。EventEmitter 的核心就是事件触发与事件监听器功能的封装。

```js
// 引入 events 模块
var events = require('events')

var EventEmitter = events.EventEmitter

var event = new EventEmitter()

event.on('some_event', function(){
  console.log('某个事件触发')
})

setTimeout(function(){
  event.emit('some_event')
}, 1000)
```



/* 坚持自己，我这样挺好啊 */

我们来具体看下 EventEmitter 的属性

`addListener(event, listener)`   为指定的事件添加一个监听器到监听器数组的末尾

`on(event, listener)` 同上

`once(event, listener)` 为指定的事件添加一个单次监听器，该监听器只会触发一次，触发后立刻解除该监听器

`removeListener(event，listener)` 移除指定事件的某个监听器，该监听器 必须是该事件已经注册过的

`removeAllListeners([event])` 移除所有事件的所有监听器，如果指定事件，则移除指定事件的所有监听器

`setMaxListeners(n)`  默认情况下，EventEmitters 如果添加的监听器的个数超过 10 个就会出现 警告 的信息，setMaxListeners 用于提高监听器默认的限制数量

`listeners(event)` 返回指定事件的监听器 **数组** 

`emit(event, [arg1],[arg2],[...])` 按参数的顺序执行每个监听器，如果有事件注册返回 true , 否则返回 false

`listenerCount(emitter, event)` 返回指定事件的监听器数量， **这个是类方法**

`newListener` event -事件名称；listener-事件处理函数



### error事件

EventEmitter 定义了一个特殊的事件 error，它包含了错误的语义，我们在遇到 异常的时候通常会触发 error 事件。

当 error 被触发时，EventEmitter 规定如果没有响 应的监听器，Node.js 会把它当作异常，退出程序并输出错误信息。

我们一般要为会触发 error 事件的对象设置监听器，避免遇到错误后整个程序崩溃。例如：

```js
var events = require('events')
var event = new events.EventEmitter()

event.emit('error')
```



### 继承 EventEmitter

大多数时候我们不会直接使用 EventEmitter，而是在对象中继承它。包括 fs、net、 http 在内的，只要是支持事件响应的核心模块都是 EventEmitter 的子类。



为什么要这样做呢？原因有两点：

- 首先，具有某个实体功能的对象实现事件符合语义， 事件的监听和发射应该是一个对象的方法。
- 其次 JavaScript 的对象机制是基于原型的，支持 部分多重继承，继承 EventEmitter 不会打乱对象原有的继承关系。
