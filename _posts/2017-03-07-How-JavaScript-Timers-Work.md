---
layout: post
title:  "关于JavaScript计时器的工作原理"
date:   2017-03-07 01:30:00
categories: 前端技术
tags: JavaScript 笔记
---

* content
{:toc}

使用setTimeout和setInterval分别完成计时功能时，我开始思考二者之间的区别。在查看翻阅相关资料后，我对于JavaScript计时器的工作原理乃至异步javascript执行的工作原理都有了进一步的认识。



## 例子

**setInterval()** 

```
<script type="text/javascript">
	var t=0;
	setInterval(function clock(){
		t+=1;
	},1000)
</script>
```
**setTimeout()**

```
<script type="text/javascript">
	var t=0;
	setTimeout(function clock(){
		t+=1;
		setTimeout(clock(),1000);
	},1000)
</script>
```
**比较**

上述两种方式其实现的目的相同，看似都是每隔1000ms进行一次回调，然而 setInterval 和 setTimeout 在JS执行过程中实际上有很大区别的。
首先使用 setTimeout 的方法，JS中将在每一次回调执行之后经过至少1000ms（时间可能更多，如存在点击事件之类）之后再次回调，而 setInterval 则力求将每次回调时间都控制在1000ms（看似回调时间控制更精确，其实有一定缺陷存在）每隔1000ms，便发起一次回调。
要理解这之间的原因，首先要对JavaScript计时器的工作原理有所了解。

## 计时器的工作原理

**先贴上一张重要图片**
![alt text](http://omem0e1o1.bkt.clouddn.com/Timers.png "Timers")

认真阅读上图后能很清晰的看出JS在单线程性质下处理异步事件的过程：

<strong>由于单线程的性质，JS一次只能够执行一段代码，可以把它看作主进程。而当异步事件发生时，JS并不会立刻执行，而是将异步事件放到一个等待队列中，等待主进程的空闲回调。</strong>

因此计时器的延迟是不能被保证的。当数字变得越来越大时，由代码冻结和线程阻塞造成的的延时也将被放大。

**回到计时器本身**

```
setTimeout（function（）{ 
/ * Some long block of code ... * / 
setTimeout（arguments.callee，10）; 
}，10）;
```
```
setInterval（function（）{ 
/ * Some long block of code ... * / 
}，10）;
``` 
 在上述代码中，实际上 setTimeout 和 setInterval 计时器都是在代码块完成之前被触发的，但因为线程，他们不会被立即执行，而是强制放到异步队列中，等待主程序执行的空闲处插入回调。 setTimeout 在上一个回调执行之后，代码将有至少10ms的延迟。

但 setInterval 并不会等待上一次的回调结束再向队列中插入回调，而是尝试每隔10ms便执行一次回调。那么这就产生了一个问题，当上一个回调尚未被处理时，而间隔被再次触发，此时第二个回调将无法加入等待队列而被直接删除。从这点上看，使用 setTimeout 或许更为安全。

当然，在间隔长于延迟时，两者都可以无延迟的连续执行。

## 总结

计时器本身并不难，但要做到精准就要充分的理解它的工作原理。了解JavaScript引擎的工作原理，是处理好异步的关键，也是为编写更高级复杂的程序打下基础。（码完这篇学习笔记已是深夜，如有错误，回头再做修改。）

## 附录

**参考文章**

[How JavaScript Timers Work](http://ejohn.org/blog/how-javascript-timers-work/)

**相关**

[用JS实现活动精确倒计时](http://www.xuanfengge.com/js-realizes-precise-countdown.html)

