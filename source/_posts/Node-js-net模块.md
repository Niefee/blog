---
title: Node.js net模块
date: 2018-09-20 10:15:08
tags: Node.js
categories: 笔记 
---

## net模块

net模块是同样是nodejs的核心模块。http模块功能继承或者依赖于net模块。

net模块组成：
1. net.Server
tcp/server, 服务端TCP监听来自客户端的请求，并使用TCP连接(socket)向客户端发送数据；
内部通过socket来实现与客户端的通信；


2. net.Socket
tcp/本地，客户端TCP连接到服务器，并与服务器交换数据；
socket的node实现，实现了全双工的stream的接口；

> 链接：https://juejin.im/post/5a713d4051882573351a9d72

参考：

> [Nodejs进阶：核心模块net入门与实例讲解](https://segmentfault.com/a/1190000007507322)
> [Node.js文档](http://nodejs.cn/api/net.html#net_server_close_callback)