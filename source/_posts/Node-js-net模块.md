---
title: Node.js net模块
date: 2018-09-20 10:15:08
tags: Node.js
categories: 笔记 
---

## net模块

net模块是同样是nodejs的核心模块，http模块功能继承或者依赖于net模块。
net对应传输层，http对应应用层。

net模块组成：

1. **net.Server**: tcp/server, 服务端TCP监听来自客户端的请求，并使用TCP连接(socket)向客户端发送数据；
内部通过socket来实现与客户端的通信；


2. **net.Socket**: tcp/本地，客户端TCP连接到服务器，并与服务器交换数据；
socket的node实现，实现了全双工的stream的接口；

###  服务端net.Server
```js
let net = require('net')
let PORT = 8081
let HOST = 'localhost'
/**
 * 1. 创建一个TCP服务器实例，调用listen函数开始监听指定端口；
 * 2. 传入net.createServer()的回调函数，作为connection事件的处理函数；
 * 3. 在每个connection事件中，该回调函数接收到的socket对象是唯一的；
 * 4. 该连接自动关联一个socket对象
 * */
let server = net.createServer((socket) => {
    console.log('connection:' + socket.remoteAddress, socket.remotePort)
    // 为这个socket实例添加一个“data”事件处理函数
    socket.on('data', (data) => {
        console.log('DATA' + socket.remoteAddress + ":" + data);
        socket.write('You said "'+ data +'"\r\n') // 向客户端回发该数据

        // 如果想浏览器收到数据，可以如下发送：
        /*
        socket.write(`
			HTTP/1.1 200 ok
			Content-Length: 11

			hello,world
		`);*/
    })
    
    /**
     * 服务端收到客户端发出的关闭连接请求时，会触发end事件
     * 这个时候客户端没有真正的关闭，只是开始关闭；
     * 当真正的关闭的时候，会触发close事件；
     * */
    socket.on('end', () => {
        console.log('客户端关闭')

        // 调用了该方法，则所有的客户端关闭跟本服务器的连接后，将关闭服务器
        // server.unref();
    })
    
    // 客户端关闭事件
    socket.on('close', () => {
        console.log('CLOSED: ' + socket.remoteAddress + ' ' + socket.remotePort);
    })
    
    // 设置客户端超时时间，如果客户端一直不输入，超过这个时间，就认为超时了
    socket.setTimeout(3000)
    socket.on('timeout', () => {
        console.log('超时了')
        // 默认情况下，当可读流读到末尾的时候会关闭可写流
        socket.pipe(socket, {end: false})
    })
})

server.listen(PORT, HOST, () => {
    console.log('服务端的地址是：', server.address())
})

server.on('error', (err) => {
    console.log(err)
})
```

服务端也可以通过显式处理"connection"事件来建立TCP连接，只是写法不同，二者没有区别。
```js
let server = net.createServer()
server.listen(PORT,HOST)
server.on('connection', (socket) => {
	console.log('CONNECTED: ' + sock.remoteAddress +':'+ sock.remotePort);
})
server.on('close', () => {
	//关闭服务器，停止接收新的客户端的请求
	console.log( 'close事件：服务端关闭' );
})

server.on('error', (error) => {
	console.log( 'error事件：服务端异常：' + error.message );
})
```

### 客户端net.Socket

```js
let net = require('net')

//创建一个TCP客户端连接到刚创建的服务器上，该客户端向服务器发送一串消息，并在得到服务器的反馈后关闭连接。

var client = new net.Socket()
let PORT = 8081
let HOST = 'localhost'

client.connect(PORT, HOST, () => {
	console.log('connect to ' + HOST + ':' + PORT)
	client.write('I am happyGloria.') //建立连接后立即向服务器发送数据，服务器将收到这些数据
})

client.on('data', (data) => {
	console.log('DATA: ' + data)

	// 完全关闭连接，没有关闭会导致超时。
	client.destroy() 
})

client.on('close', function () {
	console.log('Connection closed')
})
// client.end()
```
> 链接：https://juejin.im/post/5a713d4051882573351a9d72

参考：

> [Nodejs进阶：核心模块net入门与实例讲解](https://segmentfault.com/a/1190000007507322)
> [Node.js文档](http://nodejs.cn/api/net.html#net_server_close_callback)
