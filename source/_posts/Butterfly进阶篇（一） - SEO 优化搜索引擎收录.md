---
title: Butterfly 进阶篇（一） - SEO 优化搜索引擎收录
tags:
  - 
  - 
categories:
  - 博客
description: Butterfly主题安装的进阶内容，用过SEO完成优化搜索引擎对个人博客的收录
keywords: 'Butterfly, hexo, 魔改, SEO, 搜索引擎收录, 百度收录, 谷歌收录, 必应收录'
abbrlink: 2a1b5a62
date: 2022-09-04 10:00:00
updated:
top_image:
cover:
---
# 前言

我们必须把我们的网站推送到搜索引擎那， 否则别人除了输入我们的域名或者搜索文章，是没法发现我们的博文。

本篇设置基于Butterfly主题4.4.0版本

> 本文主要参考[Hexo 框架 (六)：SEO 优化及站点被搜索引擎收录设置 | juanertu.com](https://blog.juanertu.com/archives/9013c8d8.html)
>
> 详细视频教程参考这个大佬的[相关视频](https://www.bilibili.com/video/BV1W34y1o7yK/?spm_id_from=333.788&vd_source=8bba695aa4490252230ffd2e2cc0609b)

# 1. 查看是否被收录

使用想要查找的搜索引擎，输入：

```
site:你的网站
比如我的：site:qmike.top
```

# 2. 永久化URL网址链接

> 我们可以发现 hexo 默认生成的文章地址路径是 【网站名称／年／月／日／文章名称】。
>
> 这种链接对搜索爬虫是很不友好的，第一它的 url 结构超过了三层，太深了。

安装`abbrlink`插件：

```bash
npm install hexo-abbrlink --save
```

关于此插件的详细信息参见它的[官方文档](https://github.com/rozbo/hexo-abbrlink)。作用是将文章的链接转换成数字后字母，即将博客网站的网页转成`.html`永久链接的格式，有利于搜索引擎的收录。

修改hexo根目录下`config.yml`中的`permalink`的值：

```yml
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://qmike.top
permalink: posts/:abbrlink.html
```

在`config.yml`最底下添加`abbrlink config`

```yml
# abbrlink config
abbrlink:
  alg: crc32      # support crc16(default) and crc32
  rep: hex        # support dec(default) and hex
# 不用添加其它代码
```

配置完成后，网站的链接应该类似这样：

```
https://qmike.top/posts/77940e6f.html        # 有.html后缀 
```

# 3. 站点地图

站点地图即 [sitemap](https://baike.baidu.com/item/sitemap/6241567?fr=aladdin)， 是一个页面，上面放置了网站上需要搜索引擎抓取的所有页面的链接。站点地图可以告诉搜索引擎网站上有哪些可供抓取的网页，以便搜索引擎可以更加智能地抓取网站。所以我们首先需要生成一个站点地图。

安装百度和 Google 的站点地图生成插件：

```bash
npm install hexo-generator-baidu-sitemap --save
npm install hexo-generator-sitemap --save
```

然后来到hexo根目录配置文件`config.yml`，在下面添加：

```yml
# 站点地图
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```

然后重新推送到服务器，访问如下 URL:

```
https://你的域名/sitemap.xml
https://你的域名/baidusitemap.xml
```

看看网页中有没有出现代码。有的话就成功。

> 注意代码中的域名是否和自己网站的一样，使用`github page`部署的网站，可能会出现域名不同的情况，需要之前完成token令牌密钥的验证，[视频](https://www.bilibili.com/video/BV1W34y1o7yK/?spm_id_from=333.788&vd_source=8bba695aa4490252230ffd2e2cc0609b)中有介绍。

给你的 hexo 网站添加蜘蛛协议 robots.txt, 把 robots.txt 放在你的 hexo 站点的 source 文件下即可。

```
# hexo robots.txt
User-agent: *
Allow: /

Sitemap: https://qmike.top/sitemap.xml
Sitemap: https://qmike.top/baidusitemap.xml
```

# 4. 百度收录

## 提交网站

通过百度站长平台进行链接提交，增加网站的索引量。先去注册并登录：[百度站长平台](https://ziyuan.baidu.com/?castk=LTE=)

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904180119988.png" alt="image-20220904180119988" style="zoom: 33%;" />

需要验证网站，我选择的是 https://，这根据你前面是否添加 SSL 证书来选择。并且我使用的是不带 www 的，看个人。然后到第三步，我使用的 HTML 标签验证。

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904181206160.png" style="zoom: 80%;" />

把 `content` 中的字符串复制到主题配置文件`_config.butterfly.yml`中的 `baidu_site_verification` 。

```yml
# Baidu Webmaster tools verification.
# See: https://ziyuan.baidu.com/site
site_verification:
  # - name: google-site-verification
  #   content: xxxxxx
  - name: baidu-site-verification
    content:  # 在这里填上面的字符串
```

> 需要将网站部署完后，再去百度站长平台完成HTML 标签验证

## 提交链接

百度站长平台的链接提交方式分为自动提交和手动提交两种，此处只讲自动提交，手动提交按照要求操作即可。

**主动推送**最为快速的提交方式，是被百度收录最快的推送方式。主动推送可以通过安装插件实现：

```bash
npm install hexo-baidu-url-submit --save
```

然后在hexo根目录配置文件`_config.yml`中，添加：

```yml
# 主动推送百度，被百度收录
baidu_url_submit:
  count: 10 # 提交最新的10个链接
  host: # 百度站长平台中注册的域名
  token: # 秘钥，百度站长平台 > 普通收录 > 推送接口 > 接口调用地址中token字段
  path: baidu_urls.txt # 文本文档的地址， 新链接会保存在此文本文档里，不用改
```

- host为自己网站的域名，例如我的为`https://qmike.top`

- token需要打开“普通收录-->推送接口”进行查看

  <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904212055771.png" alt="image-20220904212055771" style="zoom: 67%;" />

其次，记得查看hexo根目录中`_config.yml` 文件中` url`的值， 必须包含是百度站长平台注册的域名。

最后，在`_config.yml` 文件中的 `deploy`加入新的`type`:

```yml
deploy:
  - type: git
    repository: https://github.com/fenshen000/fenshen000.github.io.git
    branch: main
  - type: baidu_url_submitter
```

> 这里是新建一个type，一定要注意这段代码里面各行的缩进值

其主动推送的实现原理如下：

- 新链接的产生， `hexo generate` 会产生一个文本文件，里面包含最新的链接

- 新链接的提交， `hexo deploy` 会从上述文件中读取链接，提交至百度搜索引擎

  > 不知道对于部署在Netlify上的网站有没有用，再查查资料

若要实现手动提交，则把下面的代码粘贴到百度站长平台的“手动收录”地址窗口即可：

```
https://你的域名/sitemap.xml
https://你的域名/baidusitemap.xml
```

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904213924274.png" alt="image-20220904213924274" style="zoom: 50%;" />

后续慢慢等收录吧，百度收录比较慢。

# 5. 谷歌收录

提交谷歌搜索引擎比较简单，在提交之前，我们依然可以使用 `site:域名` 查看网站是否被收录。进入[Google搜索中心](https://developers.google.com/search#?modal_active=none)，登录你的谷歌账号。然后找到[注册Search Console](https://search.google.com/search-console/welcome)(在“使用入门-->SEO新手指南”中可以找到入口)，就直接输入你要收录的网站域名就行。

详细操作参考谷歌的[官方指南](https://support.google.com/webmasters/answer/9008080#html_verification&zippy=%2C%E5%9F%9F%E5%90%8D%E6%8F%90%E4%BE%9B%E5%95%86%2Chtml-%E6%A0%87%E8%AE%B0%2Chtml-%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0)

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904220444787.png" alt="image-20220904220444787" style="zoom: 67%;" />

选择第一个或者第二个都可以的，我这里两个都选择了。

“网址前缀”验证很简单，输入网址`https://qmike.top`即可直接验证。“网域”验证较为复杂，点击“继续”后，操作如下：

> 可以添加所有的网址变体，包括https，http，www和非www变体

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904221520736.png" alt="image-20220904221520736" style="zoom:67%;" />

打开你的域名提供商网站，在里面添加“解析设置”。以阿里云为例：

- 打开域名的“解析设置”，点击“添加记录”

  <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904224419062.png" alt="image-20220904224419062" style="zoom: 40%;" />

- “记录类型”选择“TXT”，“主机记录”选择“@”，记录值写入上面复制的TXT记录值

  <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220904225057831.png" alt="image-20220904225057831" style="zoom: 67%;" />

- 重新部署后返回谷歌页面进行验证，可能需要等待一段时间。

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/20200403223509.png" alt="20200403223509" style="zoom: 80%;" />

两种方式，你可以下载个 HTML 文件然后放在站点目录下的 `source` 中，然后推送到服务器。或者把 `content` 中的字符串复制到主题配置文件`_config.butterfly.yml`对应内容中：

```yml
site_verification:
  - name: google-site-verification
    content: # 在这里填上面的字符串
  - name: baidu-site-verification
    content: XXXXX
```

> 部署网站到Netlify，一天时间便会自动收录

# 6. 必应收录

必应收录也是很简单，点击[必应站长](https://www.bing.com/webmasters/about)。先注册登录，必应收录有两种方式，一种使用刚刚谷歌导入过去，第二种是就是自己添加 URL

# 7. 其它收录

其他搜索引擎的收录都很类似，就不一一赘述了。

# 8. 添加nofollow标签

给非友情链接的出站链接添加「nofollow」标签，nofollow 标签是由谷歌领头创新的一个「反垃圾链接」的标签，并被百度、yahoo 等各大搜索引擎广泛支持，引用 nofollow 标签的目的是：用于指示搜索引擎不要追踪（即抓取）网页上的带有 nofollow 属性的任何出站链接，以减少垃圾链接的分散网站权重。

```bash
npm install hexo-filter-nofollow --save
```

再在hexo根目录的`_config.yml` 中添加配置，将 `nofollow` 设置为 `true`：

```yml
nofollow:
  enable: true
  field: site
  exclude: ''
```

这样，例外的链接将不会被加上 `nofollow` 属性。









