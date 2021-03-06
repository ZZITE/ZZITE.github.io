---
layout: post
title:  "了解HTTP的基础知识"
date:   2019-12-06
categories: 外文翻译
tags: 翻译 HTTP
---

* content
{:toc}

原文：[Understanding HTTP Basics](http://www.steves-internet-guide.com/http-basics/)
2019.12.06 译




## 了解HTTP的基础知识

HTTP代表超文本传输协议，被用来通过Web传输数据。

这是一个Web开发者需要去理解的关键协议。并且因为它的广泛流传，它还被用来于物联网应用中传输数据和指令。

第一个版本的的协议只有一个方法，也就是GET，用于从服务端请求一个页面。

从服务端返回的永远是一个HTML页面。
看看这只有一页的 [Original specification](http://www.w3.org/Protocols/HTTP/AsImplemented.html)你就会明白HTTP协议在最开始的时候有多么简陋。

在最初的0.9版本之后，一共有好几个版本。

当前版本为1.1，上一次修订时间在2014年。你可以在[WiKi](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)中查看更多详细内容。

### 如何工作

与大多数Internet协议http一样，它是一个基于命令和响应文本的协议，使用客户端服务器通信模型。
![1.png](https://zzite.github.io/image/posts/WeChat9bbe2a6ac89ba9d45d74e6f3f3c7ecf3.png)
由客户端发起请求，服务端做出响应。

HTTP协议是一个无状态协议，意思是服务器并不需要去存储session信息，并且每个请求之间是完全独立的。查看[WiKi](https://en.wikipedia.org/wiki/Stateless_protocol)

这意味着：

* 所有请求发起于客户端（你的浏览器）
* 服务器响应请求
* 请求（指令）和响应都是可读的文本
* 请求之间是独立的并且服务端不需要跟踪请求

### 请求和响应结构

请求和响应消息结构是相同的，如下所示：
![2.png](https://zzite.github.io/image/posts/WeChat7d5c9531b5946d8c59148ad792958709.png)

一个请求的组成：

一个指令或请求 + 可选头 + 可选主体内容

一个响应的组成：
一个状态码 + 可选头 + 可选主体内容

一个简单的CRLF（回车换行）组合用来划分部分，单个空行（CRLF）表示头部的结尾。

*消息正文在请求中的存在由Content-Length或Transfer-Encoding头字段表示。 请求消息框架独立于方法语义，即使该方法未定义消息主体的任何用法。 – [RFC7230](https://httpwg.org/specs/rfc7230.html) 3.3节*

**注解：消息正文后没有CRLF 见[RFC7230](https://httpwg.org/specs/rfc7230.html) 3.5节**

### HTTP请求

在早些时候我们看到了一般请求响应的格式，现在让我们了解更多关于请求的内容。

起始行是强制的结构如下：

方法 + 资源路径 + 协议版本

例如如果我们向www.testsite5.com请求一个testpage.html的web页面

请求的起始行将会是：

GET/test.html HTTP/1.1

在这里：
* GET是一个方法
* /testpage.html 是资源的相对路径
* HTTP/1.1是我们使用的HTTP协议版本

注解：

1. 相对路径不包含主域名
2. Web浏览器使用我们输入的URL创建资源的相对URI。

注解：URL(统一资源定位器)用于web网页，是URL（统一资源指示器）的一个例子。

真实的HTTP请求并不会展示在浏览器上，只有使用如 http header live  (Firefox)之类的特定工具才可见。

### HTTP vs URL

大多数的人习惯在浏览器输入一个URL，通常看起来是这样的:
![3.png](https://zzite.github.io/image/posts/WeChatc76aa401b8ed761b7c78f91686b232f4.png)

这个URL也可以包含一个端口号。它通常会被浏览器所隐藏，但是你可以手动的引入它如下：
![4.png](https://zzite.github.io/image/posts/WeChat4498e9f6dd8614f6e69da8787c04bcea.png)

这将告诉Web浏览器要定位的资源的地址以及用于检索该资源（http）的协议。

http是将资源（网页，图像，视频等）从服务端传输到客户端的传输协议。

### HTTP 响应和响应码

**每一个请求都有一个响应。**响应由这些组成：

* 状态码和描述
* 至少1个的可选头
* 可选内容可以是包含二进制数据的多行内容

响应状态代码分为5组，每组都有一个含义和一个三位数代码。

* 1xx - 报告
* 2xx - 成功
* 3xx - 多项选择
* 4xx - 客户端错误
* 5xx - 服务端错误

例如一个成功的页面请求将会返回200响应码而失败的话则会返回400状态码

你可以在[这里](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)找到一个完整的列表以及他们的含义

### 请求响应示例

我们将通过请求一个简单的网页（testpage.html）来测试响应和请求。

这里是我在浏览器地址栏输入的内容：

![5.png](https://zzite.github.io/image/posts/WeChat39702ead10ccfcb7432d08a931afb7a8.png)

这是在浏览器上显示的响应内容：

![6.png](https://zzite.github.io/image/posts/WeChat68cf32594f261e1873b0e6c7607e7ac7.png)

下面是一个http 请求-响应的幕后过程截图
![7.png](https://zzite.github.io/image/posts/WeChat54e97d889797a55c4d29d7f4279436bb.png)

请注意，请求标头是由浏览器自动插入的，响应标头也是由Web服务器插入的。

这里在请求中没有主体内容。返回的主体内容为网页，并且展示在了浏览器中，并不需要通过live headers tool查看。

### 请求类型

到目前为止我们还没有提到请求类型，但我们在之前的示例中已经见到了GET类型的请求。

GET请求类型或者说方法用于向web服务器请求资源文件。

GET是最常被使用的请求类型，并且曾经是[Original HTTP specification.](http://www.w3.org/Protocols/HTTP/AsImplemented.html)里唯一的请求类型。

### 请求类型，方法或动作

HTTP协议现在支持8中请求类型，在文档中也称为方法或动作，他们分别是：
* GET - 从服务端请求资源
* POST - 提交资源到服务端
* PUT - 作为POST但替换资源
* DELETE - 从服务端删除资源
* HEAD - 作为GET但是只返回头部不包含内容
* OPTIONS - 获取资源的选项
* PATCH - 将修改应用于资源
* TRACE - 执行消息的回环

在当今的互联网 GET（获取网页）和 POST（提交表单）方法是最常用到的。

在使用Web和IOT API时，将使用其他方法，特别是PUT DELETE和HEAD.

[w3 school](https://www.w3schools.com/tags/ref_httpmethods.asp)有很好的基本概述，Microsoft [MDN site](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)更详细地介绍了它们。

[Part 2 HTTP headers](http://www.steves-internet-guide.com/http-headers/)

### 相关教程和资源
* [The TCP/IP protocol suite for beginners](http://www.steves-internet-guide.com/internet-protocol-suite-explained/)
* [Using Curl for Testing IOT Applications](http://www.steves-internet-guide.com/using-curl-iot-applications/)
