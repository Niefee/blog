---
title: events-时间触发器
date: 2018-10-16 15:09:35
tags: Node.js
categories: 笔记 
---

## events - 事件触发器

事件发生器的实例方法`on`用来监听事件，实例方法`emit`用来发出事件。

```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('触发事件');
});
myEmitter.emit('event');
```

## Event Emitter 接口的部署

Event Emitter 接口可以部署在任意对象上，使得这些对象也能订阅和发布消息。

```js
var EventEmitter = require('events').EventEmitter;

function Dog(name) {
  this.name = name;
}

Dog.prototype.__proto__ = EventEmitter.prototype;
// 另一种写法
// Dog.prototype = Object.create(EventEmitter.prototype);

var simon = new Dog('simon');

simon.on('bark', function () {
  console.log(this.name + ' barked');
});

setInterval(function () {
  simon.emit('bark');
}, 500);
```

## emitter.prependListener(eventName, listener) 方法


添加 `listener` 函数到名为 `eventName` 的事件的监听器数组的开头。

```js
server.prependListener('connection', (stream) => {
  console.log('已连接');
});
```

## emitter.once(eventName, listener) 方法

添加单次监听器 `listener` 到名为 `eventName` 的事件。 当 `eventName` 事件下次触发时，监听器会先被移除，然后再调用。

```js
server.once('connection', (stream) => {
  console.log('第一次调用');
});
```

## 响应函数的数量

 - `EventEmitter.defaultMaxListeners`： 默认值为10， 表示每个事件的最多可以绑定的响应函数数量。需要注意的是，当修改它时，会影响所有 EventEmitter 的实例。

 - `emitter.listenerCount(eventName)`：获取事件 eventName 已绑定的响应函数个数。

 - `emitter.setMaxListeners(n)`：修改 emitter 的每个事件最多可以绑定的响应函数数量，该方法会修改 `emitter._maxListeners` 的值，其优先级大于 `EventEmitter.defaultMaxListeners`。

 - `emitter.getMaxListeners()`：获取 emitter 每个事件最多可以绑定的响应函数数量。

## 其他相关方法

 - `emitter.eventNames()`：返回当前已经绑定响应函数的事件名组成的数组。

 - `emitter.listeners(eventName)`：返回 eventName 事件的响应函数组成的数组。

 - `emitter.prependOnceListener(eventName, listener)`：类似于 once()，不过会将响应函数插到当前该事件处理函数队列的头部。

 - `emitter.removeAllListeners([eventName])`：移除 eventName 事件所有的响应函数。当未传入 eventName 参数时，所有事件的响应函数都会被移除。

 - `emitter.removeListener(eventName, listener)`：移除 eventName 事件的响应函数 listener。

## newListener 和 removeListener 事件

当 emitter 被注册响应函数时，会触发 newListener 事件；被移除响应函数时，会触发 removeListener 事件。

```js
const EventEmitter = require('events');

let emitter = new EventEmitter();

// 注意：此处使用 emitter.on 方法的话会陷入循环调用，导致栈溢出
emitter.once('newListener', (event, listener) => {
    if (event === 'hi') {
        emitter.on('hi', () => {
            console.log('Nice to meet you.');
        });
    }
});

emitter.on('hi', (name) => {
    console.log(`My name is ${name}!`);
});

emitter.emit('hi', 'elvin');
```

> 参考：
> http://javascript.ruanyifeng.com/nodejs/events.html
> http://nodejs.cn/api/events.html
> http://imweb.io/topic/5973722452e1c21811630609