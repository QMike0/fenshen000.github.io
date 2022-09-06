---
title: VScode添加GitBash终端
tags:
  - null
  - null
categories:
  - VScode
description: 在新版VScode的终端中添加GitBash，注明了相关的注意事项
keywords: 'VScode, vscode, gitbash, vscode终端'
abbrlink: 77940e6f
date: 2022-09-04 17:00:00
updated:
top_image:
cover:
---

# 前言

VScode的终端中没有包含Git Bash，但预留了它的位置。本文将演示如何在设置中添加Git Bash终端。

> 本文适用于VScode 1.71.0 版本及其它较新版本

# 操作步骤

1. 文件->首选项->设置，打开设置
2. 搜索`shell windows`

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/1.png" alt="1" style="zoom:50%;" />

3. 打开settings.json在里面输入代码如下：

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904170153395.png" alt="image-20220904170153395" style="zoom: 90%;" />

注意两点：

- settings.json中原先为`"Git Bash"`，需要删除空格，例如改为`"GitBash"`
- 删除`"GitBash"`中的`"Source"`，只保留`"path"`

4. 保存重启vscode，按ctrl+~键打开终端，完成

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904170717210.png" alt="image-20220904170717210" style="zoom: 50%;" />