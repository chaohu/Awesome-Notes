<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Nodejs Basic Notes](#nodejs-basic-notes)
	- [Npm Set Up](#npm-set-up)
		- [Basic Steps](#basic-steps)
		- [Test Steps](#test-steps)
		- [Publish Steps](#publish-steps)
		- [Tab Completion](#tab-completion)
	- [Basic Node Modules](#basic-node-modules)
		- [Process Object](#process-object)
	- [File Module](#file-module)
		- [fs API](#fs-api)
		- [Buffer Object](#buffer-object)
		- [Path API](#path-api)
	- [Self-Defined Modules](#self-defined-modules)
		- [Export Modules](#export-modules)
	- [Http Module](#http-module)
		- [Resquest Object](#resquest-object)
			- [属性](#属性)
		- [Response Object](#response-object)
			- [类型](#类型)
			- [事件](#事件)
			- [方法](#方法)
		- [Http Get](#http-get)
		- [Http Server](#http-server)
	- [Net Module](#net-module)
		- [Socket Object](#socket-object)
		- [Basic Methods](#basic-methods)
	- [URL Module](#url-module)
		- [Basic Method](#basic-method)
	- [Async](#async)
	- [Awesome Package](#awesome-package)
		- [Http](#http)
		- [Stream](#stream)
		- [Format](#format)

<!-- /TOC -->

# Nodejs Basic Notes

## Npm Set Up

### Basic Steps

```shell
$ npm adduser
$ mkdir proj/
$ npm init --scope=<username>  // 修改 package.json 可再次运行此命令

$ npm install --save <modulename>     // 修改 package.json 可再次运行此命令(不接模块名为自动更新)
$ npm prune                    // 清除无用包
$ npm rm --save  // --save 删除文件的同时更新 package.json 文件

$ npm ls
$ npm outdated   // 去除过期包
```

### Test Steps

```json
// in package.json
"scripts": {
    "test": "node test.js"
},
```

```shell
$ npm test
```

### Publish Steps

```shell
$ npm publish
$ npm dist-tag add @<pkg>@<version> [<tag>]
$ npm dist-tag rm <pkg> <tag>
$ npm dist-tag ls [<pkg>]

```

### Tab Completion

```shell
npm completion >> ~/.bashrc (or ~/.zshrc)
source ~/.zshrc
```

## Basic Node Modules

### Process Object

```js
process.pid：当前进程的进程号。
process.version：Node的版本，比如v0.10.18。
process.platform：当前系统平台，比如Linux。
process.title：默认值为“node”，可以自定义该值。
process.argv：当前进程的命令行参数数组。
process.env：指向当前shell的环境变量，比如process.env.HOME。
process.execPath：运行当前进程的可执行文件的绝对路径。
process.stdout：指向标准输出。
process.stdin：指向标准输入。
process.stderr：指向标准错误。
```

## File Module

### fs API

```js
var fs = require('fs');
var buf = fs.readFileSync('/path/to/file', [charSet]);
fs.readFile('/path/to/file', [charSet], function callback(err, dataBuf) {});
fs.readdir('/path/to/file', function callback(err, fileNameArr) {});

fs.createReadStream();

src.pipe(dst1).pipe(dst2).pipe(dst3);  //  连接多个 stream
```

### Buffer Object

```js
var str = buf.toString();
```

### Path API

```js
var path = require('path');

console.log(path.extname("index.html"));   // .html

path.normalize(p)
path.join([path1], [path2], [...])
path.resolve([from ...], to)
path.relative(from, to)
path.dirname(p)
path.basename(p, [ext])
path.extname(p)
path.sep
path.delimiter
```

## Self-Defined Modules

### Export Modules

```js
module.exports = function (args) { /* ... */ }
```

## Http Module

### Resquest Object

#### 属性

```js
request.method  // POST GET
```

### Response Object

#### 类型

```c
typedef Stream response
```

#### 事件

-   监听事件

```js
response.on('data', function (data) {});
response.on('error', function (error) {});
response.on('end', function () {
    // 结束阶段
    stream.end();
});
```

-   发出事件

```js
response.end();  //  传输结束
```

#### 方法

```js
response.setEncoding('utf8');  // 自动将 data 事件中 Buffer 对象转换成 String

//  content-type: text/plain
//                application/json
response.writeHead(200, { 'Content-Type': ''});
```

### Http Get

```js
http.get(url, function callback(response) { });
```

```js
http.get(url, function (response) {
    var pipeData = '';

    response.setEncoding('utf8');
    response.on('data', function (data) {
        pipeData += data;
    });
    response.on('end', function () {
        console.log(pipeData.length);
        console.log(pipeData);
    });
});
```

### Http Server

```js
var server = http.createServer(function (request, response) {
    // 处理请求的逻辑...
});
server.listen(8000);
```

## Net Module

### Socket Object

```js
socket.write(data);
socket.end(data);
socket.end();
```

### Basic Methods

```js
var serverInstance = net.createServer(function callback (socket) {});

serverInstance.listen(portNumber);   // 开始监听特定端口
```

## URL Module

### Basic Method

```js
url.parse(request.url, true);
```

## Async

对回调进行计数是处理 Node 中异步的基础 - 自定义 Semaphore 变量: 每完成一个异步处理, Semaphore++

## Awesome Package

### Http

-   bl
-   concat-stream
-   async

### Stream

-   through2-map

### Format

-   strftime
