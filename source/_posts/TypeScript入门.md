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
枚举可以通过编号与名称互换，即(name -> value）和（value -> name）。

```js
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
console.log(c); // 2

enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];
console.log(colorName); // Green
```
> 默认从`0`开始。

### Any

在编程阶段不清楚数据类型，可以用`any`类型来标记。

```js
let notSure: any = 4;
notSure = "a string";
notSure = false; // boolean

let list: any[] = [1, true, 'hi']; // 当包含不同数据，也可以使用any
```

`any`类型可以赋任何值，也行调用当中的方法；
`Object`只能赋值，不能调用当中的方法；

```js
let notSure: any = 4;
notSure.ifItExists(); // okay, ifItExists might exist at runtime
notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)

let prettySure: Object = 4;
prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.
```

### Void

当一个函数没有返回值，可用`void`标记。声明一个`void`变量，只能复制`undefined`与`null`。

```js
function sayhi(): void {
    alert("hello world");
}
```

### Null 和 Undefined

默认情况下`null`和`undefined`是所有类型的子类型。 就是说你可以把 `null`和`undefined`赋值给`number`类型的变量。

指定`--strictNullChecks`标记，`null`和`undefined`只能赋值给`void`和它们各自。

### Never

`never`类型表示的是那些永不存在的值的类型。 

抛出异常或不会有返回值的函数表达式或箭头函数表达式的返回值类型；
`never`类型是任何类型的子类型，可以赋值给任何类型，但其他任何类型不能赋值给`never`类型。

```js
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```

### 类型断言

类型断言类似与类型转换。

```js
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
// 或
let strLength: number = (someValue as string).length;
```
