---
layout: post
title: "HTML基本元素"
tag: html
category: essay
---

**标签**：由尖括号包围而成的关键词，如`<html>`

- 有的标签是成对出现的，如`<b>` 和`</b>`，前一个称为**开始标签**，后一个称为**结束标签**
- 有的标签单独出现，如`<br>`

**元素**：HTML元素指从开始标签到结束标签之间的所有代码，如`<p>This is a paragraph</p>`；

- 开始标签和结束标签之间的内容时元素的**内容**，如上例的`This is a paragraph`；内容中可以包含HTML标签
- 某些HTML元素有空内容，如`<br />`

**属性**：属性以键值对形式 (name = "value")出现，它们为HTML元素提供了更多信息，如`<a href="http://www.baiud.com">This is a link</a>`

- 始终为属性值加引号，可以为双引号`"`或单引号`'`

- 某些属性对大多数HTML元素适用，如
  - `class`: 规定元素的类名
  - `id`: 规定元素的唯一id
  - `style`: 规定元素的行内样式
  - `title`: 规定元素的额外信息 (可在悬停时显示)