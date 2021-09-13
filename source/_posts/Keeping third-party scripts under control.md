---
title: Keeping third-party scripts under control
categories: 翻译
tags:
  - third-party
  - performance
date: 2021-09-11
cover: https://w.wallhaven.cc/full/rd/wallhaven-rdyyjm.png
---

![cover](https://web-dev.imgix.net/image/ZDZVuXt6QqfXtxkpXcPGfnygYjd2/TqyTENFItXjxfEDHLsad.png?auto=format)

在我们开始对我们项目中使用的第三方库进行优化时，我们首先要移出在项目中没有使用到的第三方依赖。

第三方库，是性能优化的一个核心关键点。但是。，在开始优化我们项目的第三方库时，我们要确保所有的第三方库在项目中都是必须使用的。而这篇文章则展示了如何通过流程来管理我们项目所使用到的第三方库。

在我们讨论第三方库的性能优化时，很容易忽略这些库的核心功能而直接跳到库的性能优化。这些第三方库提供强大的功能，使得网站 [more dynamic, interactive, and interconnected](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript)。但是，第三方库会由不同的人、不同的团队在不同的时间添加，并且在过一段时间后大家又忘记了这件事情。当团队相关人员开始流动、离职、入职时，团队不会关心流动的人在这项目所添加的第三方库。

在文章 [Improving Third-Party Web Performance](https://medium.com/the-telegraph-engineering/improving-third-party-web-performance-at-the-telegraph-a0a1000be5)，Telegraph 的 Web 团队移出了那些无法判断请求者的旧的第三方库，决定如果这个第三方库没有什么作用就从项目中移出。但是，没有人这么去做。

在思考第三方库的执行前，或者那些可以被延迟执行、或者预先执行的第三方库时，这是一个非常好的机会从管理查角度去控制第三方库的引入。一个非常常见的主题网站之所以会有性能问题，纯粹是因为这个网站是由不同的团队合作开发，然而各个团队使用了大量的第三方库，导致加载资源太过，从而造成性能问题。没有什么事情比去优化你的网站更沮丧，准备去发布你的网站更开心。我们可以通过构建第三方库添加工作流来对我们项目中使用到的第三方库进行管理。

工作流的具体管理形式依靠组织的架构和目前的处理流程。它可以就是在一个团队，由一个负责人去管理第三方库的引入和使用。或者，在团队需要引入第三方库时填写一份表单。这表单会让人填写 what、why、how long 和可以为项目带来的溢出。

## Tag governance process

一旦你开始为你的项目添加第三方库时，接下来的步骤就是第三方库的生命周期。

## Compliance

![Compliance](https://web-dev.imgix.net/image/ZDZVuXt6QqfXtxkpXcPGfnygYjd2/33aRnqMUCnbTSvaw5h0m.png?auto=format)

在我们开始为我们的项目添加一个第三方库时，检查它是否已经过法律团队的彻底审查，以确保它通过所有合规要求才能添加到我们的项目中。这可能包括检查库是否符合[EU General Data Protection Regulation (GDPR), and California Consumer Privacy Act (CCPA)](https://iapp.org/news/a/what-you-must-know-about-third-parties-under-the-gdpr-ccpa/)

这很关键，如果对此步骤有任何疑问，则需要在从性能角度评估标签之前加以解决。

## Required

![Required](https://web-dev.imgix.net/image/ZDZVuXt6QqfXtxkpXcPGfnygYjd2/kX91VwuEJzBBdf76HIm9.png?auto=format)

第二步是质疑我们项目是否真正需要第三方库，考虑以下讨论要点：

- 库是否被项目经常使用？如果不是，可以去掉吗？
- 如果库所有的工程中使用，这是否有必要？例如，如果我们正在分析 A/B 测试套件，而您目前仅在着陆页上进行测试，我们是否可以只在此页面类型上删除标记？
- 我们能否为此添加进一步的逻辑，我们是否可以检测是否存在实时 A/B 测试？如果是，则允许添加标签，但如果不存在，请确保它不存在。

## Ownership

![Ownership](https://web-dev.imgix.net/image/ZDZVuXt6QqfXtxkpXcPGfnygYjd2/VsE2wzqT56RJ7Yl7wx2P.png?auto=format)

有一个明确的人或团队作为库的所有者，主动跟踪库的使用情况。一般这人是添加库的人。通过在库旁边放置一名受让人，这将确保将来可以进行审查和审计，以重新访问是否需要库。

## Purpose

![Purpose](https://web-dev.imgix.net/image/ZDZVuXt6QqfXtxkpXcPGfnygYjd2/kKJCySoXMCTPjrID1CVg.png?auto=format)

第四步开始创建跨职能问责制和责任，确保人们理解库添加到项目的原因。对每个库给工程带来什么以及为什么使用它有一个跨职能的理解是很重要的。例如，如果库正在记录用户会话操作以允许个性化，是否所有团队都知道为什么应该出现这种情况？

此外，是否有任何商业与性能权衡的讨论？如果有一个库被认为是“必需的”，因为它会带来收入。是否对速度回归损失的潜在收入进行了分析

## Review

![Review](https://web-dev.imgix.net/image/ZDZVuXt6QqfXtxkpXcPGfnygYjd2/txmJbO1xdLzfo3PYsDgZ.png?auto=format)

第五步，也是最后一步，可以说是最重要的一步是确保定期审查库。这应该取决于项目的大小、工程上的库数量及其周转时间（例如每周、每月、每季度）。这应该像优化其他网站资产（JS、CSS、图像等）一样对待，并定期主动检查。审核失败可能会导致“臃肿”的库管理器，从而减慢页面速度。恢复到高性能状态可能是一项复杂的任务，同时不回归页面上所需的功能。

![vetting](https://web-dev.imgix.net/image/ZDZVuXt6QqfXtxkpXcPGfnygYjd2/TqyTENFItXjxfEDHLsad.png?auto=format)

审查过程应该为您留下最终的库列表，这些库根据特定用途的需要进行分类。在此阶段，您可以深入研究技术优化方法。这也为在性能预算内定义此最终列表中的库数量提供了机会，可以在 Lighthouse CI 中进行监控并纳入特定于性能的目标设置。例如：

> If we stick to <5 tags on our Landing Pages along with our own optimized JS, we're confident the Total Blocking Time (TBT) can hit 'good' in the Core Web Vitals.
