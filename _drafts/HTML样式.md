---
layout: post
title: "HTML样式"
tag: html
category: essay
---

## 样式表

当浏览器读到一个样式表，他会按照这个格式来对文档进行格式化，有三种方式插入样式表：

- **外部样式表**：

```html
<head>
    <link rel="stylesheet" type="text/css" hrefe"mystyle.css">
</head>
```

- **内部样式表**：

```html
<head>
    <style type="text/css">
        body {background-color: red}
        p {margin-left: 20px}
    </style>
</head>
```

- **内联样式**：

```html
<p style="color: red; margin-left: 20px">
    This is a paragraph
</p>
```

### 颜色

**颜色值**：颜色值由一个十六进制符号定义，这个符号由RGB三值构成

| 颜色 | Color HEX |
| ---- | --------- |
| 红色 | #FF0000   |
|绿色|#00FF00|
|蓝色|#0000FF|
|黄色|#FFFF00|
|青色|#00FFFF|
|品红色|#FF00FF|
|灰色|#C0C0C0|
|白色|#FFFFFF|

**颜色名**：大多数浏览器支持颜色名集合；HTML4.0标准仅支持16种颜色名：aqua, black, blue, fuchsia, gray, green, lime, maroon, navy, olive, purple, red, silver, teal, white, yellow

| 颜色                              | 颜色名 |
| --------------------------------- | ------ |
| <span style="color:aqua">■</span> | Aqua   |
|<span style="color:BlueViolet">■</span>|BlueViolet|

**Web安全色**：在256色时，一种216色方案的Web安全色被建议使用，以用来和微软/Mac操作系统的40中保留色区分；如今Web安全色存在的意义不大

