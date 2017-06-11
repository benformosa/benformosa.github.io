---
layout: default
title: Blog
permalink: /blog-index/
---

# Blog posts
{% for post in site.categories.blog %}
* {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ post.url | prepend: site.baseurl }})
{% endfor %}