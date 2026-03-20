---
layout: default
title: Categories
permalink: /categories/
---

# Categories

Browse posts by category:

{% assign categories = site.data.categories %}
{% for category in categories %}
  ## [{{ category.name }}]({{ site.baseurl }}/categories/{{ category.slug }})
  {{ category.description }}
  
  {% assign posts_in_category = site.posts | where: "category", category.name %}
  **Posts:** {{ posts_in_category | size }}
{% endfor %}
