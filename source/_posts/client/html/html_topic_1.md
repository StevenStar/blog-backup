---
title: 你并不真正了解的HTML HEAD
date: 2017-05-27 16:14:28
tags: HTML
category: 前端
---

# 介绍
首先参考桑大书总结的内容([链接](https://cnodejs.org/topic/5718e5685a26c4a841ecbbb6))，非常的详细，只是没有说明。更多内容请参考底部其他资源，里面有更详细的介绍。

# 基础
有些东西必须的需要加入页面head，无所谓可以不用放在代码里。
## html实例
一个简单的 HTML 文档，带有最基本的必需的元素：
```
<html>

<head>
  <title>文档的标题</title>
</head>

<body>
  文档的内容... ...
</body>

</html>
```
## 定义和用法
`<head>` 标签用于定义文档的头部，它是所有头部元素的容器。`<head>` 中的元素可以引用脚本、指示浏览器在哪里找到样式表、提供元信息等等。
文档的头部描述了文档的各种属性和信息，包括文档的标题、在 Web 中的位置以及和其他文档的关系等。绝大多数文档头部包含的数据都不会真正作为内容显示给读者。
下面这些标签可用在 head 部分：`<base>`, `<link>`, `<meta>`, `<script>`, `<style>`, 以及 `<title>`。
`<title>` 定义文档的标题，它是 head 部分中唯一必需的元素。
## 常用head
### title 标签
每个页面职能有一个标题
```
<!-- 页面的标题，必填项，如果没有，对于不同浏览器有不同的填法。 -->
<title>Hello World!</title>
```
### Meta 标签
提供搜索引擎关于页面内的重要资讯,常用有两个，description和keywords。
```
<!-- name 属性 -->
<meta name="description" content="网站的描述。。。" />
<meta name="keywords" content="关键字。。。" />
<meta name="author" content="作者名称。。。" />
<meta name="generator" content="网页编辑器名称。。。" />
<meta name="copyright" content="网页的版权或著作权声明。。。" />
<meta name="distribution" content="网页的发布地区。。。" />
<!-- 页面宽度和缩放 -->
<meta name="viewport" content="width=device-width,initial-scale=1" />
<!-- http-equiv 常用屬性 -->
<!-- 1. 网页内容的种类以及编码 -->
<meta http-equiv="Content-Type" content="text/html;charset=uft-8" />
<!-- 2. 网页使用的语言种类 -->
<meta http-equiv="Content-Language" content="zh-TW">
<!-- 3. 自动更新网页的时间 -->
<meta http-equiv="Refresh" content="10">
<!-- 4. 禁止浏览器用快取开启网页 -->
<meta http-equiv="Pragma" content="no-cache">
<!-- 5. 强制再单一视窗中显示网页 -->
<meta http-equiv="windows-Target" content="_top">

<!-- 为了万恶的IE，使用X-UA-Compatible。告诉IE要用最新的版本，如果用户安装chrome，就用Google Chrome Frame!如果不加入这行可能会在一些需要认证的网站出现错误 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
```
### Link 标签
用来控制网页内与外部资源的关联
```
<!-- 网址上面的小图标,一般浏览器会去根目录寻找favicon.ico。 -->
<link rel="icon" href="/favicon.ico" type="image/x-icon" />
<!-- 载入css -->
<link rel="stylesheet" href="css/your-css.css">
```
### Style 标签
用来定义网页所使用的style,如css样式
```
<style>
    body {
        font-size: 13px;
    }
</style>
```
### Script标签
用来使用网页script或嵌入外部script，如JavaScript或VBScript
```
<!-- 载入javascript -->
<script src="js/your-script.js"></script>
```
## 不常用head
### Base 标签
用来指定网页内URL的目标
```
<base url="/" />
```
### Noscript 标签
```
<noscript><!--no JS alternative--></noscript>
```
## html5新增的meta功能
```
<!-- 页面编码，一般不指定页面的编码时，浏览器根据服务器送来的header或者用其他方法判定，现在常用的编码方式为utf-8。 -->
<meta charset="utf-8" />
```
# 客户端必备
### 苹果ios
```
<!-- 1.禁止数字拨号 -->
<meta name="format-detection" content="telephone=no">
<!-- 2. 设置标题 -->
<meta name="apple-mobile-web-app-title" content="My App">
<!-- 3. 开启全屏运行 -->
<meta name="apple-touch-fullscreen" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<!-- 4. 设置状态栏的样式 -->
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<!-- 5. 小图标 -->
<link rel="apple-touch-icon" href="/path/to/apple-touch-icon.png">
```
### Google Android
```
<meta name="theme-color" content="#E64545">
<!-- 添加到主屏幕 -->
<meta name="mobile-web-app-capable" content="yes">
<!-- More info: https://developer.chrome.com/multidevice/android/installtohomescreen -->
<meta name="google-play-app" content="app-id=package-name">
<link rel="alternate" href="android-app://package-name/http/url-sample.com">
```
### 360浏览器
```
<!-- select rendering engine in order -->
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```
### QQ浏览器
```
<!-- Locks the screen into the specified orientation -->
<meta name="x5-orientation" content="landscape/portrait">
<!-- Display this page in fullscreen -->
<meta name="x5-fullscreen" content="true">
<!-- Page will be displayed in "application mode"(fullscreen,etc.) -->
<meta name="x5-page-mode" content="app">
```
### UC浏览器
[uc浏览器文档](http://www.uc.cn/download/UCBrowser_U3_API.doc)
```
<!-- Locks the screen into the specified orientation -->
<meta name="screen-orientation" content="landscape/portrait">
<!-- Display this page in fullscreen -->
<meta name="full-screen" content="yes">
<!-- UC browser will display images even if in "text mode" -->
<meta name="imagemode" content="force">
<!-- Page will be displayed in "application mode"(fullscreen,forbiding gesture, etc.) -->
<meta name="browsermode" content="application">
<!-- Disabled the UC browser's "night mode" in this page -->
<meta name="nightmode" content="disable">
<!-- Simplify the page to reduce data transfer -->
<meta name="layoutmode" content="fitscreen">
<!-- Disable the UC browser's feature of "scaling font up when there are many words in this page" -->
<meta name="wap-font-scale" content="no">
```
# 其他资源
* [非常详细的整理](https://github.com/joshbuchea/HEAD)
* [HTML5 Boilerplate Docs: The HTML](https://github.com/h5bp/html5-boilerplate/blob/master/dist/doc/html.md)















