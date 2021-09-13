---
title: 术语解释
author: Re-Star
authorLink: "https://github.com/trueLoving"
avatar: "https://trueloving.gitee.io/blog/avatar.png"
authorAbout: 肥宅一枚
tags:
  - css
categories: 技术
comment: false
cover: https://w.wallhaven.cc/full/8o/wallhaven-8oev1j.jpg
description: css中我们经常忽略的基本概念
date: 2021-09-07 22:50:10
---

在我们学习 css 的时候，总是会急于学习如何在我们的网站中使用 css,却很少花费时间去关注 css 的一些理论知识。

在这里，罗列出 css 中常见的术语概念

## 元素

其实就是 html 的 DOM 元素，我们通过 css 来是得我们的 DOM 元素在外观和交互上使人体验更加舒服

## 选择器

在我们去编写 css 规则作用于 DOM 时，我们需要通过一种方式去获取页面中我们想要用的 DOM 元素，这种方式就是选择器

在 css 中，选择器的种类十分多，并且不同的场景下我们可以使用不同的选择器

## 规则、属性名、属性值

规则 = 属性名 + 属性值

例如 `color:red`是一条规则，其中 `color` 是属性名，而 `red` 则是属性值

## 优先级

当同一个 DOM 元素上许许多多的 css 规则，那么就有可能发生不同的 css 规则指定同一个属性名且是不同的属性值

那么，这是就要根据选择器的优先级和属性值的优先级来决定哪条 css 规则作用于该元素

## 权重

衡量 css 选择器优先级的参数指标，权重越大，优先级越高
