---
layout: blog
title: Blog
permalink: /blog/
---

<div class="blog-container">
  <div class="filters">
    <h3>Filter by Category</h3>
    <form id="category-filters">
      {% for category in site.categories %}
        <label class="category-option">
          {{ category[0] }} ({{ category[1] | size }})
          <input type="checkbox" class="category-filter" value="category-{{ category[0] | slugify }}">
        </label>
      {% endfor %}
    </form>
  </div>

  <div class="posts">
    {% if site.posts.size > 0 %}
      {% for post in site.posts %}
        <div class="post {% for category in post.categories %}category-{{ category | slugify }} {% endfor %}">
          <h2>
            <a href="{{ post.url }}">{{ post.title }}</a> -
            {% for category in post.categories %}
              {{ category }}{% unless forloop.last %}, {% endunless %}
            {% endfor %}
          </h2>
          <p>{{ post.excerpt | strip_html }}</p>
        </div>
      {% endfor %}
    {% else %}
      <p>There are no posts yet!</p>
    {% endif %}
  </div>
</div>
