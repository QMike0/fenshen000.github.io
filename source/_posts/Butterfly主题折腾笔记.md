---
title: Butterfly主题折腾笔记
date: 2022-8-31 15:00:00
updated: 2022-9-1 17:30:00
tags:
- 
- 
categories:
- 博客

description: Butterfly主题下，博客美化过程记录
keywords: Butterfly, hexo
top_image: 
cover: 
highlight_shrink: false
---
# 引言
本篇记录自己在使用butterfly主题对博客进行美化的全过程、技巧，另外也是想写一下自己魔改这个主题的过程（毕竟个性化的才是最好的），万一以后遇到啥问题也可以返回来查一下可能的问题所在。
美化是一个非常折腾+耗时间的过程，或许本文会一直更新下去吧~（笑）

# Butterfly安装文档补充
Hexo所有的主题基本都配置了详细的基础教程，假如有相关经验的话，相信是可以很快入手的。当然我这样的小白必然会对其中一些配置方法和细节摸不着头脑，本章会记录我自己在使用[Butterfly安装文档](https://butterfly.js.org/)中遇到的问题，以及拓展的内容，其它基础操作不做描述。
## Git/npm安装区别
安装目录不同：git方式，butterfly主题安装在`themes`文件夹中；npm方式，主题安装在`node_modules `里

后续作用不同：npm安装方式方便于后续的“自动化配置“，参考这个[视频](https://www.bilibili.com/video/BV1Cb4y1773P/?spm_id_from=333.788)。不过我还没有尝试这个。

## Page/Post Front-matter

Front-matter 是 markdown 文件最上方以 --- 分隔的区域，用于指定个别档案的变数。

- Page Front-matter 用于`主页文章卡片`配置
- Post Front-matter 用于`文章页`配置

其实就是在每篇博文的markdown文档顶部加上分割线`---`，中间写上该文档的性质。具体写法：

```Front-matter
Page Front-matter:

---
title:
date:
updated:
type:
comments:
description:
keywords:
top_img:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---


Post Front-matter:

---
title:
date:
updated:
tags:
categories:
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---
```

> 各字段含义见[网页](https://butterfly.js.org/posts/dc584b87/#Page-Front-matter)

 ## 添加新页面

 例如要生成新页面`XXXX`，步骤如下：

- 前往你的 Hexo 博客的`根目录`

- 输入 `hexo new page XXXX`

- 在source文件夹中会新生成`XXXX`的对应文件夹，打开里面的index.md

- 修改这个文件：在最后一行添加 `type: "XXXX"`，另外可以修改这个子页面的`title`名称

- 在butterfly主题配置文件`_config.butterfly`中将这个子页面添加到导航菜单中，类似于：

  ```MENU
  menu:
    首页: / || fas fa-home
    归档||fas fa-list||hide:
      时间轴: /archives/ || fas fa-archive
      标签: /tags/ || fas fa-tags
      分类: /categories/ || fas fa-folder-open
    友链: /link/ || fas fa-link
    关于: /about/ || fas fa-heart
  ```
  
- 在index.md中添加`"top_img: YYYY.jpg"`，即可自定义它的顶部图像

  > 比在`_config.butterfly.yml`中定义要方便，另外注意图片格式

## 图标

Butterfly支持 [font-awesome v6](https://fontawesome.com/icons?from=io)图标。

## 图片配置技巧

对于页面顶部图的配置，除了支持用url链接外，也可以在`source`文件夹下新建`img`文件夹，将图片存储在这里面，调用格式为`"./img/XXXX.jpg"`，加载速度会快一些。





# 后续想实现的功能

- 网页预加载画面
- 日期、时间、天气时钟
- 看板娘
- 其它图标库和设置
- 一图流、视频流全局背景+全局渐变



# 可参考网址

https://azure0202.github.io/2021/10/03/Butterfly%E8%87%B4%E7%9F%A5%E8%AE%B0/

https://zfe.space/categories/%E6%95%99%E7%A8%8B

https://blog.imzjw.cn/posts/b74f504f/

https://akilar.top/posts/5b8f515f/



