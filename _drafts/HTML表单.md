---
layout: post
title: "HTML表单"
tag: html
category: essay
---

## 表单元素

`<input>`**输入**：定义一个表单控件

```html
<input type="hidden" id="you-cannot-see-me!">
```

`<select>` **选择**：定义一个选择框控件

`<option>` **选择**：定义选择框中的选项

```html
<select name="state" id="state">
    <option value="Alabama" selected>Alabama</option>
    <option value="Alaska">Alaska</option>
    <option value="California">California</option>
</select>
```

`<textarea>`**文本区域**：定义一个大文本框
- `cols`：定义文本框的竖直长度
- `rows`：定义文本框的水平长度

```html
<textarea name="bio" id="bio" cols="30" rows="10"></textarea>
```

`<button>`**按钮**：定义一个按钮
- `onClick`：定义点击时触发的事件

```html
<button type="reset" ...>
```

`<datalist>`****：定义一个特殊的文本框，提供若干个备选项供选择

`<output>`**输出**：定义运算的输出结果

`<form>`**表单**：定义一个表单

```html
<form action="show-data.php" method="post" enctype="multipart/form-data">
</form>
```

`<fieldset>`**字段集**：定义一组字段

`<legend>`**标题**：定义`<fieldset>`的标题

```html
<fieldset>
    <legend>Gender</legend>
    <input type="radio" name="gender" id="gender-male" value="male" checked>
    <label for="gender-male">Male</label>
    <input type="radio" name="gender" id="gender-female"
value="female">
    <label for="gender-female">Female</label>
</fieldset>
```

待施工……