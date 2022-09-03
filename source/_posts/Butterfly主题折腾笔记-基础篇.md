---
title: Butterfly主题折腾笔记-基础篇（更新中）
date: 2022-8-31 15:00:00
updated: 2022-9-1 17:30:00
tags:
- 
- 
categories:
- 博客

description: Butterfly主题安装的基础内容，是对于安装文档的补充和重点内容的摘取，便于像我这样的小白充分理解文档内容，个性化拓展博客网站的功能
keywords: Butterfly, hexo，安装文档
top_image: 
cover: 
highlight_shrink: false
---


# 前言
本篇记录自己在使用butterfly主题对博客进行美化的全过程、技巧，Hexo所有的主题基本都配置了详细的基础教程，假如有相关经验的话，相信是可以很快入手的。当然我这样的小白必然会对其中一些配置方法和细节摸不着头脑，本章会记录我自己在使用[Butterfly安装文档](https://butterfly.js.org/)中遇到的问题，以及拓展的内容，基础操作不做描述。

魔改内容参考[进阶篇]()

# 1. Git/npm安装区别
安装目录不同：git方式，butterfly主题安装在`themes`文件夹中；npm方式，主题安装在`node_modules `里

后续作用不同：npm安装方式方便于后续的“自动化配置“，参考这个[视频](https://www.bilibili.com/video/BV1Cb4y1773P/?spm_id_from=333.788)。不过我还没有尝试这个。

# 2. Page/Post Front-matter

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

 # 3. 添加新页面

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

# 4. 图标

Butterfly支持 [font-awesome v6](https://fontawesome.com/icons?from=io)图标。

# 5. 图片配置技巧

对于页面顶部图的配置，除了支持用url链接外，也可以在`source`文件夹下新建`img`文件夹，将图片存储在这里面，调用格式为`"./img/XXXX.jpg"`，加载速度会快一些。

> 注意不要在主题文件夹下的`source/img`文件夹中存储图片，例如`./themes/butterfly/source/img`，据说会因为主题的更新导致图片的丢失。

# 6. 本地搜索功能

我的博客启用的是“本地搜索”，安装该功能前先运行`hexo clean`。

需要安装 hexo-generator-search，根据它的[文档](https://github.com/wzpan/hexo-generator-search)去做相应配置。

```bash
npm install hexo-generator-search --save
```

然后在主题配置文件`_config.butterfly.yml`里，启用本地搜索功能：

```bash
# Local search
local_search:
  enable: true
  preload: true
  CDN:
 
```
- `enable`：是否开启本地搜索
- `preload`：预加载
  - 开启后，进入网页后会自动加载搜索文件；
  - 关闭时，只有点击搜索按钮后，才会加载搜索文件
- `CDN`：搜索文件的 CDN 地址（默认使用的本地链接）

然后重新生成页面即可查看更改。

其实如果没有其它的需要的话，到这里就可以了，默认配置就已经足够用了。

也可以在hexo根目录配置文件`_config.yml`中添加配置：

```bash
search:
  path: search.xml
  field: post
  content: true
  # 建议不要写入命令template: ./search.xml，实测会报错
```

- `path`：生成的搜索文件的路径，默认是 `search.xml`，也可以使用 json 格式，改为 `search.json`。
- `field`：搜索的范围，默认是 `post`，即只搜索发布的文章，也可以改为 `page`（搜索页面，即 page 类型的页面，不含发布的导航）或者 `all`（搜索全部）
- `content`：指是否搜索文章的内容，默认为 `true`，如果改为 `false` 的话则只搜索标题、说明等头部内容，不搜索文章的正文
- `template`（可选）：自定义 XML 模板的路径

> 若可以正常搜索，但无法正常跳转，参考[这篇文章](https://wangjiezhe.com/posts/2018-10-29-Hexo-NexT-2/#fn1)

# 7. 分割线图标替换

将图标更换为“太空飞船”。

修改butterfly主题配置文件`_config.butterfly.yml`：

```bash
hr_icon:
  enable: true
  icon: '\f197' # the unicode value of Font Awesome icon
  icon-top: -10px
```

- `icon-top`常用数值：

  -20px：图标位于分割线上方

  -10px：图标位于分割线中间

  0px：图标位于分割线下方

# 可参考网址

https://azure0202.github.io/2021/10/03/Butterfly%E8%87%B4%E7%9F%A5%E8%AE%B0/

https://zfe.space/categories/%E6%95%99%E7%A8%8B

https://blog.imzjw.cn/posts/b74f504f/

https://akilar.top/posts/5b8f515f/



