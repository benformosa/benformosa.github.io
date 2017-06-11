---
layout: default
title: Blog Posts
permalink: /blog-index/
---

{% for post in site.categories.blog %}
* {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ post.url | prepend: site.baseurl }})
{% endfor %}