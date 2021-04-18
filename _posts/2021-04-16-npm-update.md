---
title: npm 升级依赖
date: 2021-04-16 20:30:00 +0800
categories: [Tech]
tags: [frontend]
---

## npm 更新命令

`npm up` / `npm update` / `npm upgrade`

如果 `package.json` 文件里依赖库版本是类似 `^1.2.3` 这种格式，由于该版本代表 **[1.2.3, 2.0.0)** 的版本区间，在 npm 运行 `npm up xx` 的时候往往并不会更新该文件，而只是更新 `package-lock.json` 文件中的依赖版本

## 如果想将 `package.json` 中的库也更新到最新的版本

- 可以在 `npm up xx` 运行之后再次运行 `npm install xx`

- 或者直接运行 `npm up xx@^`

PS: 对于项目并不直接依赖的第三方库，只是用到的一些库的间接依赖，可以直接运行 `npm up xx` 更新其在 `package-lock.json` 中的版本
