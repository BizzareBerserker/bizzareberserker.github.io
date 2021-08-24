---
layout: post
title: "HTML标签"
tag: html
category: essay
---

- **注释**`<!-- -->`: 定义HTML文档中的注释，注释不会在浏览器中被渲染

```html
<!-- This is a comment -->
<!-- Comment will not be rendered in the browser -->
```
- 
  - **条件注释**：条件注释定义只在某些条件下执行的HTML标签，如
```html
<!--[if IE 8]>
    ... some HTML here ...
<![endif]-->
```

- **文档声明**`<!
- DOCTYPE>`： 声明当前Web文档的类型，主要供浏览器识别使用
```html
<!DOCTYPE html>
```

## TEXT

- **标题**`<h1>` `<h2>` `<h3>` `<h4>` `<h5>` `<h6>`：定义HTML标题 (Heading)

```html
<h1>This is a heading!</h1>
```

- **段落**`<p>`：(块级元素) 定义HTML**段落**，浏览器会自动在段落前后添加空行

```html
<p>This is a paragraph</p>
<p>This is another paragraph</p>
```


- **水平线**`<hr>`: 定义HTML中的水平线
```html
<p>This is a paragraph</p>
<hr>
<p>This is another paragraph</p>
```

- **折行**`<br>`: 定义HTML中的折行，这会在不产生新段落的情况下换行
```html
<p>This is a <br />paragraph with <br />line breaks</p>
```

## HTML

- **HTML文档**`<html>`：定义HTML文档
```html
<html>
    <head></head>
    <body>
    This is body.
    </body>
</html>
```

- **主体**`<body>`：定义HTML文档的主体
```html
<body>
    <p>This is my paragraph</p>
</body>
```

- **标题**`<title>`：定义文档的标题；它指 % 搜索引擎结果中显示的标题 % 工具栏中显示的标题 % 添加到收藏夹时显示的标题
```html
<head>
<title>Title of the document</title>
</head>
```

- **默认地址**`<base>`：定义所有连接的默认地址或默认目标
  - `href`: 规定所有链接的默认地址
  - `target`: 规定所有链接的默认目标
```html
<head>
<base href="http://www.w3school.com.cn/images/" />
<base target="_blank" />
</head>
```

- **外部资源**`<link>`：定义文档与外部资源之间的关系 (如引入CSS/JS等)
  - `rel`: 规定外部资源与本文档的关系
  - `type`: 规定外部资源的MIME类型
  - `href`: 规定外部资源的URL
```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

- **样式**`<style>`：定义文档的样式信息
```html
<head>
<style type="text/css">
body {background-color: yellow}
p {color: blue}
</style>
</head>
```

- **元数据**`<meta>`：定义元数据
  - `http-equiv`: 把content属性关联到HTTP头部
    - `content-type`
    - `expires`
    - `refresh`
    - `set-cookie`
  - `name`: 把content属性关联到一个名称
    - `author`
    - `description`
    - `keywords`
    - `generator`
    - `revised`
    - `others`
  - `scheme`: 定义翻译content属性值的格式

## FORMAT

### 文本格式化

- **粗体**`<b>`：定义粗体文本

- **斜体**`<i>`：定义斜体文本

- **着重**`<em>`：定义着重文字

- **加重语气**`<strong>`：定义加重语气

- **大号字**`<big>`：定义大号字

- **小号字**`<small>`：定义小号字

- **上标**`<sup>`：定义上标字

- **下标**`<sub>`：定义下标字

- **插入线**`<ins>`：定义插入字

- **删除线**`<del>`：定义删除字

### 计算机代码

- **代码**`<code>`：定义编程代码，浏览器通常使用等宽字体显示
```html
<code>
var person = {
    firstName:"Bill",
    lastName:"Gates",
    age:50
    eyeColor:"Blue"
}
</code>
```

- **键盘格式**`<kbd>`：定义键盘上的输入格式
```html
To open a file, press <kbd>Ctrl</kbd>+<kbd>C<\kbd>
```

- **样本**`<samp>`：定义计算机输出实例
```html
<samp>
demo.example.com login: Apr 12 09:10:17
</samp>
```

- **变量**`<var>`: 定义数学变量
```html
<var>E<\var>=<var>m<\var><var>c<\var><sup>2<\sup>
```

- **预格式化**`<pre>`：定义预格式化输入，\<pre\>中的中的空格和换行会保持原样输出，文本也会以等宽字体呈现
```html
<pre>
&lt;html&gt;
    &lt;head&gt;&lt;/head&gt;
    &lt;body&gt;&lt;/body&gt;
&lt;/html&gt;
</pre>
```

- **打字机效果**`<tt>`：定义类似打字机的等宽文本效果
```html
<tt>Hello!</tt>
```

### 引用

- **缩写**`<abbr>`：定义缩写词
  - `title`：定义缩写的全拼，可以再悬停时显示
```html
<abbr title="People's Republic of China">PRC</abbr> was founded in 1949.
```

- <span style="color:red">[HTML5不支持]</span>**首字母缩写**`<acronym>`：定义首字母缩写词
  - `title`：定义缩写全拼，可以再悬停时显示
```html
<acronym title="World Wide Web">WWW</acronym>
```

- **联系信息**`<address>`：定义联系信息，通常显示为斜体并添加折行；如果`<address>`位于`<body>`内，则它表示文档联系信息，如果`<address>`位于`<article>`内，则它表示文章的联系信息
```html
<address>
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>
```

- **文字信息**`<bdo>`：定义文本显示方向
  - `dir`：文本显示方向
    - `"ltr"`：从左到右显示
    - `"rlt"`：从右到左显示
```html
<bdo dir="rtl">Here is some text from right to left</bdo>
```

- **短引用**`<q>`：定义行内引用；浏览器通常会为`<q>`元素添加引号
```html
<p>WWF的目标是：<q>构建人与自然和谐共存的世界。</q></p>
```

- **长引用**`<blockquote>`：定义块级引用；浏览器通常会为`<blockquote>`元素进行缩进处理
  - `cite`：定义引用来源
```html
<blockquote cite="http://www.worldwildlife.org/who/index.html">
五十年来，WWF 一直致力于保护自然界的未来。
世界领先的环保组织，WWF 工作于 100 个国家，
并得到美国一百二十万会员及全球近五百万会员的支持。
</blockquote>
```

- **著作标题**`<cite>`：定义著作标题
```html
<p><cite>The Scream</cite> by Edward Munch.</p>
```

- **定义**`<dfn>`：定义一个定义
```html
<p><dfn title="World Health Organization">WHO</dfn> was founded in 1948.</p>
```

## 资源

- **超链接**`<a>`：定义HTML超链接；这些连接可以跳转到外部文档、图片或者文档中的某一个部分
  - `href`: 链接的地址
  - `name`: 锚的名称；跳转到超链接时可以直接跳转到指定的锚
  - `target`: 被链接的文档如何显示
    - `"_blank"`：在新窗口中显示
```html
<a href="http://www.baidu.com">This is a link</a>
```

- **图像**`<img>`：定义HTML图像
  - `src`: 定义图像的来源URL
  - `width`: 定义图像宽度；`height`: 定义图像高度
  - `alt`: 定义替代文本；当图像无法显示时浏览器将显示替代文本
```html
<img src="photo.jpeg" width="400" height="600" />
```
- **脚本**`<script>`：定义客户端脚本
```html
<script>
document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>
```

- **脚本的替代内容**`<noscript>`：为不支持客户端脚本的用户定义替代内容
```html
<noscript>
Sorry, Your Browser does not support JavaScript!
</noscript>
```

## BLOCK

- **内联框架**`<iframe>`：定义在网页内的内嵌网页
  - `src`: 内嵌网页的URL
  - `height`: 内嵌框架的高度
  - `width`: 内嵌框架的宽度
  - `frameborder`: 是否显示内嵌框架的边缘
```html
<iframe src="demo_iframe.html" name="iframe_a">
</iframe>
```

- **行内元素**`<span>`：inline元素，本身没有语义，通常用来对文本添加CSS样式
```html
<span style="color: red">This is red text.</span>
```

- **块级元素**`<div>`：块级元素，本身没有语义，通常用来对元素块添加CSS样式或者用来布局
```html
<div id="section">
<h1>London</h1>
<p>
London is the capital city of England.It is the most populous city in the United Kingdom with a metropolitan area of over 13 million inhabitants.
</p>
</div>
```

- **页眉**`<header>`：定义文章或节的页眉
```html
<header>
<h1>Welcome to my homepage!</h1>
<p>My name is Donald Duck</p>
</header>
```

- **导航**`<nav>`：定义导航链接的容器
```html
<nav>
<a href="index.asp">Home</a>
<a href="html_meter.asp">Previous</a>
<a href="html5_noscript.asp">Next</a>
</nav>
```

- **节**`<section>`：定义文章中的节
```html
<section>
    <h1>PRC</h1>
    <p>The People's Republic of China</p>
</section>
```

- **文章**`<article>`：定义独立的自包含文章
```html
<article>
    <h1>Internet Explorer 9</h1>
    <p>Windows Internet Explorer 9 (aka. IE9) was released in March 14th, 2001</p>
</article>
```

- **侧栏**`<aside>`：定义内容之外的内容（比如侧栏）
```html
<p>Me and my family visited the Epcot center this summer</p>
<aside>
    <h4>Epcot Center</h4>
    The Epcot Center is a theme park in Disney World, Florida.
</aside>
```

- **页脚**`<footer>`：定义文章或节的页脚
```html
<footer>
    <p>Posted by: W3School</p>
    <p>Contact Information: <a href="mailto:someone@example.com">someone@example.com</a>.</p>
</footer>
```

- **细节**`<details>`：定义额外的细节

- **总结**`<summary>`：定义details元素的标题
```html
<details>
<summary>Copyright 2011.</summary>
<p>All pages and graphics on this web site are the property of W3School.</p>
</details>
```