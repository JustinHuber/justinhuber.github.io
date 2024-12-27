---
layout: mypost
title: blog搭建及使用
categories: [blog]
---

# blog选型分类
静态网站
动态网站  
github 免费 静态网页
选择主题模板
考虑因素：
学习成本
美观
访问速度

本主题研究
# 目录结构
。。。TODO
可优化点:
分页  留言功能

markdown 自定义

/static/css/post.css
可自行优化，自行学习css样式修改
h1 h2 样式统一了 写作时只需一个#，优化before 元素置为了空
h3 h4 ... h6 一样 ###

e.g
# 一个#
## 两个#
### 三个#
#### 四个#




# 如何写blog
# 使用

文章放在`_posts`目录下，命名为`yyyy-MM-dd-xxxx-xxxx.md`，内容格式如下

```yaml
---
layout: mypost
title: 标题
categories: [分类1, 分类2]
---
文章内容，Markdown格式
```

文章内容，Markdown格式
文章资源放在posts目录，如文章文件名是2024-12-14-theme-usage.md，则该篇文章的资源需要放在posts/2024/12/14下，创建时可用 \  在文章使用时直接引用即可。当然了，写作的时候会提示资源不存在忽略即可

![这是图片](xx.png)

[xxx.zip 下载](xxx.zip)
