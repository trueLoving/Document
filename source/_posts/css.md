---
title: css
author: Re-Star
authorLink: "https://github.com/trueLoving"
avatar: "https://trueloving.gitee.io/blog/avatar.png"
authorAbout: 肥宅一枚
tags:
  - css
categories: 技术
comment: false
cover: https://s3.bmp.ovh/imgs/2021/09/64986db36ad323b6.png
description: css选择器究竟是什么东西，或许因为太过常见导致我们忽视了它
date: 2021-09-06 22:50:10
---



## 前言

**css** 选择器，其用途是选择页面上的 **DOM** 元素。通过选择器，我们可以选择一个或者一类 **DOM** 元素添加我们想要的 **css** 属性，以此能够对特定的 **DOM** 元素实现样式美化

## 种类

css 选择器有不同的种类，能够让我们在各种场景下灵活使用

- 标签选择器
- 类名选择器
- 伪类选择器
- 伪元素选择器
- 属性选择器

## 优先级

若不同的选择器（选择器组）作用于同一个 DOM 元素，我们应该怎么处理

那么，这个时候我们需要计算选择器（选择器组）的权重来判断选择器的优先级

权重越大，优先级越高

## 组合选择器

不同的选择器进行组合，以此来确定选择的 DOM

例如 `.text-center .bold` 表示选择 class 既包含 `text` 也包含 `bold` 的 DOM 元素才会作用下组合选择器里定义的 css 规则
