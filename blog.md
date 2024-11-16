---
layout: blog
title: Blog
permalink: /blog/
---

<h1>Blog</h1>

<h1>Blog</h1>

{% if site.posts.size > 0 %}
  <ul>
    {% for post in site.posts %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        <p>{{ post.excerpt }}</p>
      </li>
    {% endfor %}
  </ul>
{% else %}
  <p>There are no posts yet!</p>
{% endif %}