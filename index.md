---
layout: page 
title: Recent Posts 
---

{% for post in site.posts limit: 10 %}
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <p class="author">
    <span class="date">{{ post.date | date: "%m-%d-%Y" }}</span>
  </p>
  <div class="content">
    {{ post.content }}
  </div>
{% endfor %}
