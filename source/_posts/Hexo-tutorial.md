---
title: 解决Aurora主题的若干问题的方法
date: 2023-01-20 18:05:02
tags: 
 - 教程
 - Hexo
 - 建站
feature: true
cover: https://s1.ax1x.com/2023/01/20/pSGAKE9.jpg
---

写这个主要是因为这个主题确实折腾了好久，这里就算作是备忘吧。  

这篇一共解决了三个问题：

- 首先是 /about 的问题，直接访问 /about 会出现404的问题
- 其次是在 Vercel 部署的时候主页404的问题
- 最后是在大部分页面刷新报404的问题

# Github库的修改  

因为本站是文件在Github上然后部署在Vercel上，所以这一部分的话不用Vercel是可以直接跳过了。  

这里我首先参考了 [这个Comment][Comment1]。发现需要创建Vercel.json。  

然后呢，我就按照它的内容直接复制了，发现过不了Vercel的检查。  

查了下才发现，是Vercel方面更新了Config的格式。

在它的文档里弃用了route这个写法，转为了其他的属性去代替它。  

在翻阅的时候，看到它的文档里恰好有这个示例，所以就直接复制，发现有用。

内容如下：

```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}

```

这里贴一张截图，文档链接[在这][Vercel-doc]
![pSGkf1K.png][doc-pic]

# _config.aurora.yml的修改

这步主要为了解决刷新404的问题。

在Aurora的官方文档里写了这样一句:

> 修改 permalink 参数为 /post/:title.html

在翻issue的过程中发现，有人指出这种写法是不对的 (当时还在解决Vercel的404问题，就没太注意，所以Issue链接也找不到了)

应该改为 `/post/:title` 而不应该加上html后缀。


```yml
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://tridiamond.tech
permalink: /post/:title
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks

```

# About 404的解决

其实很简单，只需要在上面加上`type: about`就能很好解决。

```markdown
---
title: about
type: about
---
```
这样就可以直接解决了！


[Comment1]: https://github.com/auroral-ui/hexo-theme-aurora/issues/78#issuecomment-844790557
[Vercel-doc]: https://vercel.com/docs/project-configuration#legacy/routes
[doc-pic]: https://s1.ax1x.com/2023/01/20/pSGkf1K.png