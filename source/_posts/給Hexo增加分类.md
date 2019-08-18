---
title: 給Hexo增加分类
date: 2019-07-21 16:55:47
tags:
- hexo
- Web
categories:
- Web
halftitle: hexo-categories
---
# 添加分类功能
其实Hexo自带有归档功能categories，不过要先对配置文件进行一些修改。
## 使用方法
### 生成（文章）时默认生成categories配置项
**categories有点类似tags，写在文章属性之中，所以需要在文章生成时添加categories属性。编辑`/scaffolds/post.md`，在最下面添加一行categories**
``` shell
title: {{ title }}
date: {{ date }}
tags:
categories:
```
### 在生成文章后编辑categories属性
**在新建文章后，编辑categories属性：**
``` shell
title: Hexo添加归档/分类功能
date: 2016-11-02 19:41:27
tags: [Hexo,Blog]
categories: 技巧经验
```
**这样在文章发布后，使用hexo g命令，hexo会在根目录/public/categrises下自动生成归档文件夹**
<!--more-->
**以上，这样其实就成功添加了分类功能。不过这样添加的分类只能显示在文章的属性中，没有从首页直接查看分类的方法。以下提供一种实现方法**
### 分类功能可视化
**以Yilia主题为例，在主题配置文件`themes/_config.yml`中添加以下代码（#号后为注释内容）:**
``` shell
menu:
  主页: /
  所有文章: /archives
  技巧经验: /categories/技巧经验     # 博客首页展示文本： 访问路径/自定义归档名称
  资料总结: /categories/资料总结
```
**然后执行`hexo clean && hexo g && hexo s`就可以看到效果了。**


