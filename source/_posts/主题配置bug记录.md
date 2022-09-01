---
title: butterfly主题配置bug记录
date: 2022-9-1 17:53:00
updated: 
tags:
- 
- 
categories:
- 
- 

highlight_shrink:
description: 总能遇到千奇百怪的bug，算是一本“怪物图鉴”了吧
keywords: Butterfly, bug, hexo
top_image: 
cover: 
highlight_shrink: false
---
# 引言
世界上除了学不完的知识，还有排不完的bug。。

本篇记录自己在使用butterfly主题时遇到的各种报错，每个都是独一无二且千奇百怪的

排除bug是一个非常折腾+耗时间的过程，或许本文会一直更新下去吧~（恼）

# YAMLException: bad indentation of a mapping entry 
```报错示例
# 运行hexo g后出现如下报错
YAMLException: bad indentation of a mapping entry (7:20)

 4 |
 5 | menu:
 6 |   首页:/ || fas fa-home
 7 |   菜单 || fas fa-list:
------------------------^
 8 |     时间轴: /archives/ || fas fa-archive
 9 |     标签: /tags/ || fas fa-tags
    at generateError (D:\Blog\悠悠の哉\node_modules\js-yaml\lib\loader.js:183:10)
    at throwError (D:\Blog\悠悠の哉\node_modules\js-yaml\lib\loader.js:187:9)
    ...
```

```原因&解决方法
报错原因：一般是英文冒号后缺失空格
解决方法：通过报错找到相应位置，添加空格
```
> 这或许是目前遇到的最多的报错了吧。。

# warning: adding embedded git repository: XXXX

```报错示例
# 运行git add .后出现如下报错
warning: adding embedded git repository:xxxxxxxxxx
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint:
hint: git submodule add <url>xxxxxxxxxx
hint:
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint:
hint: git rm --cached   xxxx
hint:
hint: See "git help submodule" for more information.
```

```原因&解决方法
报错原因：没有添加相应的子模块，在.gitmodules中没有这个子模块的path和url信息。
        经常出现在配置完主题，却没有添加子模块的情况。
解决方法：以主题`butterfly`为例，运行如下指令：
        # 如果是文件
        git rm --cached themes/butterfly
        # 如果执行以上命令后若提示：【 error: 如下文件其暂存的内容和工作区及 HEAD 中的都不一样：】 ，`-f`强制删除
        git rm -f --cached themes/butterfly

		#=添加仓库索引=======================================
		# 创建子模块并添加butterfly的url地址
		# 格式为git submodule add <url> <path>
		git submodule add https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
		# 或者也可以使用butterfly的ssh地址
```



