---
layout: default
title: Categories
permalink: /categories/
---

# Categories

Browse posts by category:

{% assign categories = site.data.categories %}
{% for category in categories %}
## [{{ category.name }}]({{ '/categories/' | append: category.slug | append: '/' | relative_url }})
{{ category.description }}

{% assign posts_in_category = site.posts | where: "category", category.name %}
**Posts:** {{ posts_in_category | size }}

{% endfor %}
