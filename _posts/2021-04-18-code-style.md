---
title: 代码风格
date: 2021-04-18 22:00:00 +0800
categories: [Tech]
tags: [frontend]
---

## JavaScript 语句后应该加分号么

真正会导致上下行解析出问题的 `token` 有 5 个：括号、方括号、正则开头的斜杠、加号、减号(**+ - / ( [**)，实际代码几乎没有正则，加号，减号作为行首的情况，所以总结下来：一行开头是括号或者方括号的时候在行首加上分号。

## script 标签能否放到 body 之后

Google 并没有把 `<script>` 插入在 `</body>` 之后，而只是没有写 `</body>` 和 `</html>` 闭合标签。这样做是符合标准的，不仅是 HTML5 标准，从第一个 HTML 正式标准 HTML 2.0 开始，这样做都是允许的，在 `</body>` 之后插入其他元素，从 HTML 2.0 起就是不合标准的。

按照 HTML5 标准中的 HTML 语法规则，如果在 `</body>` 后再出现 `<script>` 或任何元素的开始标签，都是 parse error，浏览器会忽略之前的 `</body>`，即视作仍旧在 body 内。所以实际效果和写在 `</body>` 之前没有区别。

## Typescript

- 能用 `interface` 的全用 `interface`，除非只能用 `type` (函数声明用 `type`)
- 能用 `undefined` 的全用 `undefined`，除非只能用 `null`，因为：
  - null + 1 // 1
  - typeof null // 'object'
  - typescript 可选参数 (arg?: xxx)
  - 未定义自然被赋值 undefined，或没有获取到对象属性
  - json 减小体积
  - 默认参数，如果传 `null` 则认为传递了值，其值为 `null` 而默认值不起作用
