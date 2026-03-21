---
layout: default
title: Blog
permalink: /blog/
---

# All Posts
{% for post in site.posts %}
- **[{{ post.title }}]({{ post.url | relative_url }})**<span class="post-meta">{% if post.category %} — <a href="{{ '/categories/' | append: post.category | downcase | append: '/' | relative_url }}">{{ post.category }}</a>{% endif %} — {{ post.date | date: "%B %d, %Y" }}</span>
{% endfor %}
