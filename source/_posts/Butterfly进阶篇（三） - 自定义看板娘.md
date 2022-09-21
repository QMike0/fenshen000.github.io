---
title: Butterfly进阶篇（三） - 自定义看板娘
tags:
  - null
  - null
categories:
  - 博客
description: Butterfly主题安装的进阶内容，自定义live2d模型，也就是左下角的“小当家”看板娘
keywords: 'Butterfly, hexo, 魔改, 看板娘, live2d, live2d模型'
abbrlink: 6cf9df4b
date: 2022-09-22 00:20:00
updated:
top_image:
cover:
---
# 前言

基于live2d模块，用最基础的方式为博客安装看板娘，更高阶的方法和模型请参考[店长的教程](https://akilar.top/posts/5b8f515f/)。

本篇设置基于Butterfly主题4.4.0版本。

# 1. 安装

在Hexo根目录下打开终端，输入以下指令安装必要插件。

```bash
npm install --save hexo-helper-live2d
```

打开站点配置文件`config.yml`
搜索`live2d`,按照如下注释内容指示进行操作。
如果没有搜到`live2d`的配置项，就直接把以下内容复制到最底部。

```yml
# Live2D
## https://github.com/EYHN/hexo-helper-live2d
live2d:
  enable: true #开关插件版看板娘
  scriptFrom: local # 默认
  pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
  pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
  pluginModelPath: assets/ # 模型文件相对与插件根目录路径
  # scriptFrom: jsdelivr # jsdelivr CDN
  # scriptFrom: unpkg # unpkg CDN
  # scriptFrom: https://npm.elemecdn.com/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
  tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
  debug: false # 调试, 是否在控制台输出日志
  model:
    use: live2d-widget-model-wanko # npm-module package name
    # use: wanko # 博客根目录/live2d_models/ 下的目录名
    # use: ./wives/wanko # 相对于博客根目录的路径
    # use: https://npm.elemecdn.com/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
  display:
    position: left #控制看板娘相对位置
    width: 180 #控制看板娘大小
    height: 360 #控制看板娘大小
    hOffset: 0 #控制看板娘平行位置
    vOffset: -100 #控制看板娘垂直位置
  mobile:
    show: true # 手机中是否展示
  react:
    opacity: 0.85 #设置透明度
```

完成后保存修改，在Hexo根目录下运行指令

```bash
hexo clean
hexo g
hexo s
```

> 注意必须要使用hexo clean是因为我们需要清空缓存重新生成静态页面，不然看板娘没被加入生成的静态页面里，是不会出现的。

# 2.更换看板娘

同样是在Hexo根目录下打开终端，选择想要的看板娘进行安装，例如我这里用到的是 `live2d-widget-model-wanko`，一个装在碗里的小狗狗。其他的模型也可以在[模型预览](https://huaji8.top/post/live2d-plugin-2.0/)里查看以供选择。

输入指令

```bash
npm install --save live2d-widget-model-wanko
```

然后在站点配置文件`_config.yml`里找到`model`项修改为期望的模型。

```yml
model:
  use: live2d-widget-model-wanko
  # 默认就是live2d-widget-model-wanko
```

之后重新运行就可以预览效果

```
hexo clean
hexo g
hexo s
```

如果要调整看板娘的大小、位置等，在`config.yml`中修改`live2d`的配置项。
