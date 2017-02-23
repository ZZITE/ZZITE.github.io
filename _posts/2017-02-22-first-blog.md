---
layout: post
title:  "第一篇博客"
date:   2017-02-22 21:17:00
categories: 日常
tags: 记录 闲谈 
---

* content
{:toc}

于知乎偶然看得答主 [高浩阳](https://www.zhihu.com/people/gaohaoyang/answers) 展示的个人博客，并在其 [Github](https://github.com/Gaohaoyang/gaohaoyang.github.io/blob/master/README-zh-cn.md) 源码仓库，根据所提供的使用方法搭建本博客。有兴趣的朋友可以点击上述链接查看。再次感谢开源，也希望有一天自己有能力独自重构此博客。



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

代码风格与 GitHub 上 README 或 issue 中的一致。使用3个\`\`\`的方式。