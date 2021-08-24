---
layout: post
title: "HTML媒体"
tag: html
category: essay
---

## 画布

`<canvas>`**画布**：绘制一块画布。canvas元素本身没有绘图能力，需要依靠JavaScript执行。Canvas图形是逐像素进行渲染的，不支持事件处理器，适合图像密集型的游戏。

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

`<svg>`**可伸缩矢量图形**：定义一个内嵌的SVG图形。SVG是一种使用XML描述2D图形的语言，SVG支持事件处理器，但复杂度过高会减慢渲染速度。

```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
    <polygon points="100,10 40,180, 190,60 10,60 160,180" 
    style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;">
</svg>
```

## 媒体

### 视频格式

|格式|文件|描述|
|---|---|---|
|MPEG|`.mpg` `.mpeg`|跨平台，普及|
|MPEG-4|`.mp4`|新的普及格式，得到HTML5支持|
|WMV|`.wmv`|需要Windows组件，普及|
|AVI|`.avi`|Windows支持，普及|
|QuickTime|`.mov`|苹果公司开发|
|RealVideo|`.rm` `.ram`|适合低带宽|
|Flash|`.swf` `.flv`|Macromedia开发|

### 音频格式

|格式|文件|描述|
|----|----|----|
|Wave|`.wav`|普及，所有Windows+Browser(/Chrome)支持|
|MP3|`.mp3` `.mpga`|有压缩格式，MPEG的声音部分|
|WMA|`.wma`|无压缩格式，普及|
|RealAudio|`.rm` `.ram`|适合低带宽|
|MIDI|`.mid` `.midi`|仅包含数字指令，文件小|

### 插件

`<object>`**对象**：定义一个HTML嵌入式对象（如Applet, PDF阅读器，Flash播放器或一个嵌入式网页等）

- `data`: 数据源

```html
<object width="100%" height="500px" data="snippet.html"></object>
```

`<embed>`**嵌入式对象**：定义了嵌入式对象

- `src`：数据源

```html
<embed src="audi.jpg">
```

### 媒体

#### 音频

I. 使用`<embed>`元素：（可能需要浏览器安装插件以提供技术支持）

```html
<embed height="100" width="100" src="song.mp3">
```

II. 使用`<object>`元素：（可能需要浏览器安装插件以提供技术支持）

```html
<object height="100" width="100" data="song.mp3"></object>
```

III. <img src="C:\repo\template\SuperTinyIcons\images\reference\html5.svg" width="25" height="25"> 使用`<audio>`元素：

```html
<audio controls="controls">
    <source src="song.mp3" type="audio/mp3" />
    <source src="song.ogg" type="audio/ogg" />
    Your browser does not support this audio format
</audio>
```
- `<source>`：定义媒体文件来源
  - `src`：媒体文件路径
  - `type`：媒体文件类型

#### 视频

I. 使用`<embed>`元素：（可能需要浏览器安装插件以提供技术支持）

```html
<embed height="100" width="100" src="movie.swf">
```

II. 使用`<object>`元素：（可能需要浏览器安装插件以提供技术支持）

```html
<object height="100" width="100" data="movie.swf"></object>
```

III. <img src="C:\repo\template\SuperTinyIcons\images\reference\html5.svg" width="25" height="25"> 使用`<audio>`元素：

```html
<audio controls="controls">
    <source src="movie.mp4" type="video/mp4" />
    <source src="movie.ogg" type="video/ogg" />
    <source src="movie.webm" type="video/webm" />
    Your browser does not support this video format
</audio>
```
- `<source>`：定义媒体文件来源
  - `src`：媒体文件路径
  - `type`：媒体文件类型

IV. 使用YouTube：记下视频id，在内嵌框架中让iframe指向视频的URL即可

- `autoplay`：载入页面后自动开始播放，Chrome不允许非静音情况下的自动播放；1=自动播放，0=不自动播放
- `mute`：视频默认静音；1=静音，0=不静音
- `loop`：视频循环播放；1=永远循环，0=不循环
- `controls`：视频框架是否显示播放器控件；1=显示控件，0=不显示控件

```html
<iframe width="420" height="315" 
    src="https://www.youtube.com/embed/ih1l6wb7LhU">
</iframe>
```
