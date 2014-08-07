---
layout: default
permalink: /journal/
---

Journal
=======

A collection of useful writings, rants, and random thoughts.

{% for post in site.posts %}
  <div class="journal-entry">
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    {% if post.date %}
      <time datetime="{{page.date}}"> {{post.date | date: "%F"}}</time>
    {% endif %}
    <div class="excerpt">{{ post.excerpt }}</div>
  </div>
{% endfor %}
