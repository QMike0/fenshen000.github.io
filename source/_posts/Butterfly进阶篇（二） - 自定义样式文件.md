---
title: Butterfly进阶篇（二） - 自定义样式文件
tags:
  - null
  - null
categories:
  - 博客
description: Butterfly主题安装的进阶内容，自定义网页样式文件
keywords: 'Butterfly, hexo, 魔改, CSS, 自定义样式'
abbrlink: f42db57d
date: 2022-09-20 00:17:00
updated:
top_image:
cover:
---
# 前言

通过设置css样式表自定义网站的各类样式，包括底栏、滚动条、鼠标等

本篇设置基于Butterfly主题4.4.0版本

> 参考这个大佬的[视频](https://www.bilibili.com/video/BV1ph411H7ng/?spm_id_from=pageDriver&vd_source=8bba695aa4490252230ffd2e2cc0609b)

# 1. 准备工作

在hexo博客目录的`source`文件夹中创建`css`文件夹，并在里面新建`style.css`样式表文档。

后面的所有样式就写在这个文档里面，网站会自动调用。

在修改特定样式前右键要修改的部位，点击“检查”会出现网站的样式代码，找到该位置的class名称，在`style.css`中输入class名称和相应的属性。

![image-20220905121148860](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220905121148860.png)

# 2. 修改底栏footer

将footer修改为“透明”，字体修改为“黑色”：

```
#footer{
    background: transparent;
}

#footer-wrap{
    color: #0d0d0d;
}
```

# 3. 修改滚动条和鼠标

样式文件参考[github上的代码](https://github.com/fenshen000/HexoStaticFile/tree/master/src/css)

在`style.css`样式表文档中添加代码：

```css
/* 鼠标样式 */
body {
    cursor: url(https://cdn.jsdelivr.net/gh/constown/HexoCustomFile/public/cursors/default.cur),
      default;
  }
  a,
  img {
    cursor: url(https://cdn.jsdelivr.net/gh/constown/HexoCustomFile/public/cursors/pointer.cur),
      default;
  }

  /* 滚动条样式 */
::-webkit-scrollbar {
    width: 8px;
    height: 8px;
  }
  
  ::-webkit-scrollbar-track {
    background-color: rgba(73, 177, 245, 0.2);
    border-radius: 2em;
  }
  
  ::-webkit-scrollbar-thumb {
    background-color: #49b1f5;
    background-image: -webkit-linear-gradient(
      45deg,
      rgba(255, 255, 255, 0.4) 25%,
      transparent 25%,
      transparent 50%,
      rgba(255, 255, 255, 0.4) 50%,
      rgba(255, 255, 255, 0.4) 75%,
      transparent 75%,
      transparent
    );
    border-radius: 2em;
  }
  
  ::-webkit-scrollbar-corner {
    background-color: transparent;
  }
  
  ::-moz-selection {
    color: #fff;
    background-color: #49b1f5;
  }
```



