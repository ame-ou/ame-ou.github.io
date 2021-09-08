---
title: 原型链
date: 2021-09-08 08:00:00 +0800
categories: [Tech]
tags: [frontend]
---

## 原型继承

JavaScript 对象有一个指向一个原型对象的链。当试图访问一个对象的属性时，它不仅在该对象上搜寻，还会搜寻该对象的原型，以及该对象原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或到达原型链的末尾

_遵循 ECMAScript 标准，`[[Prototype]]` 符号用于指向对象原型。从 ECMAScript 6 开始，[[Prototype]] 可以通过 `Object.getPrototypeOf()` 和 `Object.setPrototypeOf()` 访问器来访问。这个等同于 JavaScript 的非标准但许多浏览器实现的属性 `__proto__`_

## 属性

- 每个**构造函数**都有一个 `prototype` 属性，这个属性指向一个对象，也就是原型对象
- 原型**对象**默认拥有一个 `constructor` 属性，指向它的构造函数
- 每个**对象**有一个隐藏的 `__proto__` 属性，指向它的原型对象

## 说明

```js
Object.getPrototypeOf(Object.prototype); // null; 原型链顶端是 null
Object.getPrototypeOf(Object) === Function.prototype; // true; Object 作为构造函数，它的原型对象指向 Function
Object.getPrototypeOf(Function) === Function.prototype; // true
Object.getPrototypeOf("") === String.prototype; // true
Object.prototype === Object.getPrototypeOf(Function.prototype); // true; 函数原型对象的原型指向 object
```
