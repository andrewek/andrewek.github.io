---
layout: page
title: Categories
permalink: /categories/
image: cat.jpg
---

{% for category in site.categories %}
  {% capture category_name %}{{ category | first }}{% endcapture %}
  <h3>{{ category_name }}</h3>
  <div id="#{{category_name | slugize }}">
    {% for post in site.categories[category_name] %}
      <div class="category-link">
        <h5 href="{{site.baseurl}}{{post.url}}">{{post.title}}</h5>
        <p>{{post.excerpt}}</p>
      </div>
    {% endfor %}
  </div>
{% endfor %}
