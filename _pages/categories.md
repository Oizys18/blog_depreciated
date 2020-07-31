---
layout: default
title: "Categories"
author: "Oizys18"
permalink: /categories/
---

  <header class="category">
  <h1>카테고리 분류</h1>

    {% assign pages_list = site.pages %}
    {% for node in pages_list %}
    {% if node.title != null %}
    {% if node.layout == "category" %}
    {% assign this_cate = site.posts | where: "categories", node.title %}
    <a
      class="category-link {% if page.url == node.url %} active{% endif %}"
      href="{{ site.baseurl }}{{ node.url }}"
      >{{ node.title }} <span class="category-length">{{ this_cate.size }}</span></a><div class="category-content">{{node.content}}</div><br>
    {% endif %}
    {% endif %}
    {% endfor %}

  </header>
