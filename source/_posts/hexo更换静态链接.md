---
title: Hexo更换文章Url
date: 2019-08-3 18:28:57
tags: 
- hexo
categories:
- Web
halftitle: hexo-url
---
**在`scaffolds/post.md`里面增加url的标签**
```
---
title: {{ title }}
date: {{ date }}
tags:
categories:
halftitle:
--- 
```
**以后再创建文章时会生成一个half title的标签，这里就是写你的副标题的**<br>
**然后修改`_config.yml`把permalink改成halftitle即可**
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: 
root: /
permalink: :halftitle/ #:year/:month/:day/:title/
permalink_defaults:
```

