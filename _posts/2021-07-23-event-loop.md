---
title: 事件循环
date: 2021-07-23 8:00:00 +0800
categories: [Tech]
tags: [frontend]
---

## 任务队列

在事件循环中，每进行一次循环操作称为 _tick_ \
task 分为两大类, 分别是 Macro Task （宏任务）和 Micro Task（微任务）, 并且每个宏任务结束后, 都要清空所有的微任务

1. 在此次 tick 中选择最先进入队列的任务( oldest task )，如果有则执行(一次)，
   执行过程中如果遇到微任务，就将它添加到微任务的任务队列中
2. 检查是否存在 Microtasks ，如果存在则不停地执行，直至清空 Microtask Queue
3. GUI 线程接管渲染
4. 主线程重复执行上述步骤

宏任务主要包含：script( 整体代码)、setTimeout、setInterval、I/O、UI 交互事件、postMessage、MessageChannel、setImmediate(Node.js 环境) \
微任务主要包含：Promise、MutaionObserver、process.nextTick(Node.js 环境)

```js
console.log("script start");

setTimeout(function () {
  console.log("setTimeout");
}, 0);

Promise.resolve()
  .then(function () {
    console.log("promise1");
  })
  .then(function () {
    console.log("promise2");
  });

console.log("script end");
```

1. 整体 script 作为第一个宏任务进入主线程，遇到 console.log，输出 script start
2. 遇到 setTimeout，其回调函数被分发到宏任务 Event Queue 中
3. 遇到 Promise，其 then 函数被分到到微任务 Event Queue 中,记为 then1，之后又遇到了 then 函数，将其分到微任务 Event Queue 中，记为 then2
4. 遇到 console.log，输出 script end

## 为什么有宏任务和微任务的一些想法

- 微任务可以为任务区分优先级，提供插队功能
- 保证一致的执行顺序。当我们想让某几个任务异步执行，又想让彼此之间的顺序不乱，就可以使用 microtask，而不用 setTimeout
- 保证一致的执行环境。假设宏任务有可能改变数据，我们就可以把一些数据分析放到微任务中，确保使用的数据未被下一次宏任务修改。
