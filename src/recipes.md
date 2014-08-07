---
layout: default
title: Recipes
permalink: /recipes/
---

Recipes
=======

Since I'm such a lover of sharing and free knowledge, I've put up this section with recipes for stuff I cook or cooked.  I also use it to quickly share a recipe when some acquaintance asks me how something is made, and, for course, for myself in the future.  
All of these recipes are vegan-friendly.

<ul>
{% for post in site.pages %}
  {% if post.layout == "recipe" %}
    <li>
      <a href="{{ post.url | prepend: site.baseurl }}">{{post.title}}</a>
    </li>
  {% endif %}
{% endfor %}
</ul>
