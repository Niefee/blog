---
title: TypeScript入门
date: 2018-07-04 23:14:03
tags: ES6
categories: 笔记 
---

## 基本类型及定义方式

### 布尔值

只有`true`/`false`两个值。

```js
let isBool: boolean = false;
```

### 数字

TypeScript所有数字都是浮点数，支持十进制与十六进制字面量。

```js
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
```

### 字符串

字符串可以用双引号(")、单引号(')或者反引号(`)表示。

```js
let name: string = "bob";
let sentence: `hello,
my name is ${name}`;
``` 
### 数组

定义数组方法： 

 - 元素类型后加上`[]`，表示由此类型元素组成的一个数组

```js
let list: number[] = [1, 2, 3];
```


 - 使用数组泛型，`Array<元素类型>` ：

```js
let list: Array<number> = [1, 2, 3];
```

### 元组

元组类型可以表示一个已知元素的数量与类型的数组。

```js
let x: [string, number];
x = ['hello', 10]; // OK
x = [10, 'hello']; // Error
```

### 枚举

`enum`类型是对JavaScript标准数据类型的一个补充。
枚举可以通过编号与名称互换。

```js
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
console.log(c); // 2

enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];
console.log(colorName); // Green
```
> 默认从`0`开始。