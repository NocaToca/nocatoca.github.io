---
layout: blog
title: Blog
permalink: /blog/
---

<div class="posts">
  {% if site.posts.size > 0 %}
    {% for post in site.posts %}
      <div class="post">
        <h2><a href="{{ post.url }}">{{ post.title }}</a>
        -
        {% for category in post.categories %}
            {{category}}{% unless forloop.last %}, {% endunless %}
        {% endfor %}
        </h2>
        <p>{{ post.excerpt | strip_html }}</p>
      </div>
    {% endfor %}
  {% else %}
    <p>There are no posts yet!</p>
  {% endif %}
</div>

<div class="filters">
  <h3>Filters</h3>
  <form>
    {% for category in site.categories %}
      <label>
        <input type="checkbox" name="category" value="{{ category[0] }}">
        {{ category[0] }} ({{ category[1] | size }} posts)
      </label>
    {% endfor %}
  </form>
</div>
