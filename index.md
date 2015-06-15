---
layout: default
title: Chuck McCallum
---

resume: [prosaic](/resume/prose) or [poetic](/resume/verse)?

{% for post in site.posts %}

## [{{ post.title }}]({{ post.url }})
> {{ post.excerpt }}

{% endfor %}
