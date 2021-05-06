---
title: 前端基础
date: 2021-05-06 09:30:00 +0800
categories: [Tech]
tags: [frontend]
---

## script 标签

直接写在 html 中 script 标签中的 js 代码会阻塞整个页面，包括 html 结构中位于其上面的内容

`<script src="..."></script>` 不会阻塞他之前内容的渲染，但等他下载执行完后他后面的内容才会渲染

异步创建 script 不会阻塞页面渲染

script 标签 onload 在 js 文件加载并执行完毕后调用。

webpack 将多个符合 CommonJS 规范的模块打包成一个 js 文件，供浏览器执行。异步加载可通过动态创建 script 标签实现

## Time

```js
new Date().toJSON(); // 2018-08-01T07:25:06.595Z
```

## Error

async 立即执行函数捕获内部错误

```js
(async () => {
  throw "an error";
})().catch((err) => {
  console.log(err);
});
```

## Router

- hash

```js
window.location.hash = "xxx"; // 改变 hash
window.addEventListerner("hashchange", func); // 监听 hash 改变
```

- url

```js
history.pushState(obj, title, "url"); // 改变 url
window.addEventListener("popstate", func); // 监听浏览器前进后退
```

ps: 刷新浏览器网页加载对应路由内容

```js
window.addEventListener("load", func);
```

## instanceof

_instanceof_ 又叫关系运算符，用来判断某个构造函数的 _prototype_ 对象是否存在在另外一个要检测对象的原型链上

每个 js 对象都有一个 _proto_ 属性（标准表示 `[[prototype]]`)，proto 是普通对象的隐式属性，在实例化的时候，会指向 prototype 所指的对象

```js
a instanceof b; // 检查 b.prototype 是否在 a 的原型链上
```

## constructor

_constructor_ 存在于每一个 function 的 prototype 属性中，保存了指向 function 的一个引用
