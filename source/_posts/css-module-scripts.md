---
from: https://web.dev/css-module-scripts/
title: Using CSS Module Scripts to import stylesheets
author: Dan Clark
categories: 翻译
tags:
  - 翻译
  - css
keywords: ["CSS Module", "CSS"]
date: 2021.09.04
---

## 前言

根据新的 **CSS Module scripts** 特性，我们可以想在 **JavaScript** 导入[模块](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)一样去通过 `import`关键字导入 **CSS**。样式表可以跟 [constructable stylesheets](https://developers.google.com/web/updates/2019/02/constructable-stylesheets) 应用于文档或者是 [shadow roots](https://developer.mozilla.org/en-US/docs/Web/API/ShadowRoot)。这比其他导入和应用 CSS 的方式更方便、[更高效](https://dandclark.github.io/json-css-module-notes/#css-module-performancememory-examples)。

## Browser Support

CSS Module scripts 目前在 chrome & Edge 93 已经可以使用。

而在 Firefox 和 Safari 还没有得到支持。可以分别在 [Gecko bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1720570) 和 [WebKit bug](https://bugs.webkit.org/show_bug.cgi?id=227967), 处跟踪实现进度。

## Prerequisites

- 熟悉 [JavaScript modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules).
- 熟悉 [constructable stylesheets](https://developers.google.com/web/updates/2019/02/constructable-stylesheets).

## Using CSS module scripts

导入 CSS 模块脚本并将其应用到 document 或 shadow root，如下所示：

```js
import sheet from "./styles.css" assert { type: "css" };
document.adoptedStyleSheets = [sheet];
shadowRoot.adoptedStyleSheets = [sheet];
```

CSS 模块脚本的默认导出是一个 像任何其他可构造的样式表一样，它使用 usedStyleSheets 应用于文档或影子根。 ，其内容是导入文件的内容。

像任何其他 constructable stylesheet 一样，它使用 [`adoptedStyleSheets`](https://wicg.github.io/construct-stylesheets/#using-constructed-stylesheets).应用于文档或影子根。

与从 JavaScript 应用 CSS 的其他方式不同，不需要创建 style 元素或弄乱 CSS 文本的 JavaScript 字符串。

CSS 模块也有一些与 JavaScript 模块相同的好处。

- **Deduplication:** 如果从应用程序的多个位置导入相同的 CSS 文件，它仍然只会被获取、实例化和解析一次。
- **Consistent order of evaluation:** 当导入的 JavaScript 运行时，它可以依赖它导入的样式表已经被获取和解析。
- **Security:** 模块使用 [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) 获取并使用严格的 MIME 类型检查。

## Import Assertions (what's with the '`assert`'?)

导入语句的 assert { type: 'css' } 部分是 [导入断言](https://v8.dev/features/import-assertions)。这是必需的；没有它，导入将被视为正常的 JavaScript 模块导入，如果导入的文件具有非 JavaScript MIME 类型，则导入将失败。

```js
import sheet from "./styles.css"; // Failed to load module script:
// Expected a JavaScript module
// script but the server responded
// with a MIME type of "text/css".
```

## Dynamically imported stylesheets

您还可以使用[动态导入](https://v8.dev/features/dynamic-import#dynamic)导入 CSS 模块，并为类型添加一个新的第二个参数：'css' 导入断言：

```js
const cssModule = await import("./style.css", {
  assert: { type: "css" },
});
document.adoptedStyleSheets = [cssModule.default];
```

**Gotchas!**

注意， `cssModule.default` (不是 `cssModule` 本身) 添加 `adoptedStyleSheets`方法.。这是因为 通过动态 `import()`返回的对象是一个模块命名对象。 `CSSStyleSheet`是默认导出该模块的,因此是通过 `cssModule.default`访问的.

## `@import` rules not yet allowed

目前 CSS @import 规则在可构造的样式表中不起作用，包括 CSS 模块脚本。如果@import 规则存在于可构造的样式表中，则这些规则将被忽略。

```css
/* atImported.css */
div {
  background-color: blue;
}
```

```css
/* styles.css */
@import url("./atImported.css"); /* Ignored in CSS module */
div {
  border: 1em solid green;
}
```

```html
<!-- index.html -->
<script type="module">
  import styles from "./styles.css" assert { type: "css" };
  document.adoptedStyleSheets = [styles];
</script>
<div>This div will have a green border but no background color.</div>
```

规范中可能会添加对 CSS 模块脚本中的 @import 的支持。在 [GitHub issue](https://github.com/WICG/webcomponents/issues/870).中可跟踪此规范讨论。

## 注释

1. 可通过 js 的 import 导入 css 文件（css 文件内容就变成了 js 的一个变量）
2. 通过 `docuent.adoptedStyleSheet` 添加 css 内容

```js
import style from "./style.css" assert { type: "css" };
console.log(style); // constructable stylesheet
document.adoptedStyleSheet = [style];
```
