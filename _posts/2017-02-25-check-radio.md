---
layout: post
title:  "自定义checkbox,radio样式"
date:   2017-02-24 21:20:06
categories: 前端技术
tags: CSS Baidu_ife 笔记
---

* content
{:toc}

浏览器自带的 input:checkbox 的样式不能直接修改，但是提供的label标签带有for属性，当label标签被选中后，for所绑定的对应id的input也将被选中，所以可以利用这一点，来设置各种各样的自定义控件。



## 主要资料 

### label 标签

**概念：**

 `HTML <label>` 元素表示用户界面中项目的标题。它通常关联一个控件，或者是将控件放置在label元素内，或者是用作其属性。这样的控制称作label元素的labeled control 

**用法：**

```
<label>Click me <input type="text" id="User" name="Name" /></label>
```
或者
```
<label for="User">Click me</label>
<input type="text" id="User" name="Name" />
```
### :checked 伪类

**概念：**

`:checked` CSS 伪类选择器表示任何处于选中状态的 `radio(<input type="radio">),checkbox (<input type="checkbox">)`  或 select 元素中的 option HTML元素("option")) 。用户通过点击元素或选择其他的值，可以改变该元素的 :checked 状态，并:checked属性赋给一个新的对象(例如其他的option值)。

**语法：**
```
input:checked {
  margin-left: 25px;
  border: 1px solid blue;
}
```
### ::after 伪元素

**概念：**

CSS伪元素::after用来匹配已选中元素的一个虚拟的最后子元素.通常会配合content属性来为该元素添加装饰内容.这个虚拟元素默认是行内元素。

**语法：**
```
element:after  { style properties }  /* CSS2 语法 */

element::after { style properties }  /* CSS3 语法 */
```
`::after` 表示法是在CSS 3中引入的, `::`符号是用来区分伪类和伪元素的。支持CSS3的浏览器同时也都支持CSS2中引入的表示法:after

## 方法一：使用伪元素和伪类

**步骤**

隐藏 input ：
```
input{
  margin:0;
  display: none;
}
```
改变关联于 input(class="radio_a") 的 label 样式：

```
.radio{
  display: flex;
  width: 50px;
  justify-content: space-between;
}
.radio_a+label{
  width:15px;
  height: 15px;
  border:1px solid #d9d6c3;
  display:flex;
  border-radius: 50%;
}
```
添加一个伪类：
```
.radio_a:checked+label{
   border:1px solid #d2553d;
}
```
伪元素：
```
.radio_a:checked+label{
   border:1px solid #d2553d;
}
```
checkbox部分：
```
.checkbox{
  margin-top: 8px;
}
.checkBox_a+label{
  width:14px;
  height:14px;
  border:1px solid #d9d6c3;
  display:flex;
}
.checkBox_a:checked+label{
   border:1px solid #d2553d;
}
.checkBox_a:checked+label::after{
  width:9px;
  height:9px;
  margin: auto;
  content: '\2714';
  color: #d2553d;
  line-height: 9px;
  font-size: 10px;
  font-weight: 700;
}
```

## 方法二：使用雪碧图

代码如下：

```
.checkBox_b+label,.radio_b+label{
  width: 16px;
  height:16px;
  border:none;
  display: inline-block;
  background:url(0.png) no-repeat;
}
.radio_b+label{
  background-position: -24px -10px;
}
.radio_b:checked+label{
  background-position: -59px -10px;
}
.checkBox_b+label{
  background-position:-24px -32px;
}
.checkBox_b:checked+label{
  background-position: -60px -32px;
}
```

### 完成效果：
[demo](http://htmlpreview.github.io/?https://github.com/ZZITE/Baidu_IFE/blob/master/2017/%E8%87%AA%E5%AE%9A%E4%B9%89checkbox%E3%80%81radio/index.html)


## 总结思考

### 伪类和伪元素

**伪类**

伪类存在的意义是为了通过选择器找到那些不存在于DOM树中的信息以及不能被常规CSS选择器获取到的信息。
伪类由一个冒号:开头，冒号后面是伪类的名称和包含在圆括号中的可选参数。
常用伪类:
``` 
:active         向被激活的元素添加样式。    
:focus          向拥有键盘输入焦点的元素添加样式。    
:hover          当鼠标悬浮在元素上方时，向元素添加样式。    
:link           向未被访问的链接添加样式。    
:visited        向已被访问的链接添加样式。    
:first-child    向元素的第一个子元素添加样式。    
:checked        向选中的控件元素添加样式
```
**伪元素**

伪元素在DOM树中创建了一些抽象元素，这些抽象元素是不存在于文档语言里的（可以理解为html源码）；
注意:css3为了区分伪类和伪元素，规定伪类前面有一个冒号，伪元素前面有两个冒号
常用伪元素。
```
::before 作为作用元素的第一个子节点插入dom中
::after  作为作用元素的最后一个子节点插入dom中
```
**区别和联系**

    * 联系：都是通过选择器为元素添加样式
    * 区别:伪元素会创建一个元素，但不是真正的Html元素，伪类相当于为一个元素创建一个class样式	

### 两种方法的比较

**方法一**

	优点：不使用图片，体积小，减少http收发次数，提高了网络性能。
	缺点：代码数量较多

**方法二**

	优点：使用方便，呈现效果与图片效果直接相关。
	缺点：体积较大，图片太大时增加网页负担。对PS有要求，需自己制作雪碧图。	






