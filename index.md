---
layout: default
---

## Recent blog posts
{% for post in site.categories.blog offset: 0 limit: 5 %}
* {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ post.url | prepend: site.baseurl }})
{% endfor %}
[More...](/blog-index/)

## Other stuff
* [About](/about/)
* [Resume](/resume/)
