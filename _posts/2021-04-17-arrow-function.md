---
title: 箭头函数
date: 2021-04-17 19:30:00 +0800
categories: [Tech]
tags: [frontend]
---

## 1. 箭头函数没有 `this` 绑定

如果箭头函数被非箭头函数包含，则 `this` 绑定的是最近一层非箭头函数的 `this`；否则，`this` 的值会被设置为全局对象

```JS
let person = {
    name: 'foo',
    age: 18,
    say: () => {
        console.log(this)       // window 对象
        console.log(this.name)  // undefined
        console.log(this.age)   // undefined
    }
}
person.say()
```

**由于箭头函数内部的 `this` 是词法作用域，由上下文确定，不能用 `call`, `apply`, `bind` 等方法改变箭头函数 `this` 的指向**

## 2. 箭头函数没有原型，不能通过 `new` 来调用

箭头函数没有 `prototype` 属性，不能实例化，即不能用 `new` 关键字调用

```js
let Foo = () => {};
let f = new Foo(); // Uncaught TypeError: Foo is not a constructor

let Bar = () => {};
console.log(Bar.prototype); // undefined
```

## 3. 没有 `arguments` 绑定

```js
const foo = function () {
  console.log(arguments);
};
foo("foobar"); // arguments 对象

const bar = () => {
  console.log(arguments);
};
bar("foobar"); // Uncaught ReferenceError: arguments is not defined
```
