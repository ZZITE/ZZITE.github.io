---
layout: post
title:  "第一篇博客"
date:   2017-02-22 21:17:00
categories: 日常
tags: 碎碎念 
---

* content
{:toc}

### 简介

这是我的第一个博客，用于记录我的学习之路以及分享我想分享的日常。希望在一点点更新与重构的过程中，享受到更多前端带来的快乐。
~~如果能通过博客再钓到妹子，那就再好不过了≖‿≖✧~~



### 文章写法

`_posts`目录下存放文章信息，文章头部注明 layout(布局)、title、date、categories、tags、author(可选)，如下：

```
---
layout: post
title:  "对这个 jekyll 博客主题的改版和重构"
date:   2016-03-12 11:40:18 +0800
categories: jekyll
tags: jekyll 端口 markdown Foxit RubyGems HTML CSS
author: Haoyang Gao
---
```

下面这两行代码为产生目录时使用
```
* content
{:toc}
```

文章中存在的4次换行为摘要分割符，换行前的内容会以摘要的形式显示在主页Home上，进入文章页不影响。

换行符的设置见配置文件`_config.yml`的 excerpt，如下：

```yml
# excerpt
excerpt_separator: "\n\n\n\n"
```

使用 markdown 语法写文章。

