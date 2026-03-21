---
layout: default
title: Personal
permalink: /categories/personal/
---

# Personal

{% assign posts = site.posts | where: "category", "Personal" %}

{% if posts.size > 0 %}
  <ul>
  {% for post in posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      — {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endfor %}
  </ul>
{% else %}
  <p>No posts in this category yet.</p>
{% endif %}

<p><a href="{{ '/categories/' | relative_url }}">← Back to Categories</a></p>
