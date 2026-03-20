---
layout: default
title: Personal Posts
permalink: /categories/personal/
---

# Personal Posts

{% assign posts = site.posts | where: "category", "Personal" %}

{% for post in posts %}
  - [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

[← Back to Categories]({{ site.baseurl }}/categories/)
